# Issue

**Title:** Honour the per-user job cap, size pipe job arrays to it, and hand a failed array's tasks to the Scheduler

## Description

## Problem

On Zeus the PBS queue enforces a per-user job cap (`max_queued = [u:PBS_GENERIC=40]`). Three things went wrong under it:

- A submission refused with `qsub: would exceed queue generic's per-user limit` was retried after a sleep, but the retry's result was discarded. When the retry was accepted, the caller still got `(None, None)`, so the job ran untracked, ARC treated it as failed and resubmitted, and the cap filled further.
- A pipe run submits one job array, and every array subjob counts against the cap. Arrays of 39 to 80 workers could never fit, so the driver waited and retried the same size indefinitely.
- A pipe array that failed to submit for any other reason stayed STAGED forever, with fresh PENDING tasks and no worker.

## What each commit changes

1. **job submission** (`arc/job/local.py`, `arc/job/ssh.py` and tests). `local.submit_job` and `SSHClient.submit_job` loop while the scheduler reports the cap (PBS `would exceed` / `Maximum number of jobs`, Slurm `AssocMaxSubmitJobLimit`), sleeping `SUBMISSION_CAP_WAIT_SECONDS` (5 min) between attempts, and return the status and job ID of the attempt that is accepted. The unused `recursion` parameter is removed. `local.submit_job(wait_on_cap=False)` returns `(SUBMISSION_CAP_REACHED, None)` at once so the caller can resize.
2. **queue allowance discovery** (`arc/job/pipe/queue_limit.py` and tests). Reads the user's remaining allowance: PBS from `qstat -Qf` / `-Bf` and the user's jobs in `qstat -w -t -u` (wide format so a truncated queue name still matches by prefix; array subjobs counted; capped at the server's `max_array_size`); Slurm from `sacctmgr`, `scontrol` and `squeue`.
3. **array sizing** (`arc/job/pipe/pipe_run.py` and tests). `PipeRun.submit_to_scheduler` starts at the size the tasks call for, limited by the allowance, halves the array while the queue refuses it, and waits for the queue only when a one-worker array is refused. The array size is stored in `run.json`.
4. **submission retry and hand-off** (`arc/job/pipe/pipe_coordinator.py` and tests, `arc/scheduler_pipe_test.py`). One `_submit` helper serves the first submission, the retries and the existing resubmission of retried tasks. A run whose array was never submitted is retried on later polls, at most `pipe_settings['max_attempts']` submissions in total, spread evenly over `SUBMIT_FALLBACK_DELAY` (600 s) so back-to-back polls do not use them up. Once they are used and the delay has passed, its PENDING tasks are ejected to the Scheduler as individual jobs, the run is marked FAILED and forgotten, and one error names the run. A failure to save the run's metadata after an accepted submission is logged and does not count as a failed submission, so it cannot cause a second array. The poll tests in `arc/scheduler_pipe_test.py` now model a submitted run.
5. **settings** (`arc/settings/settings.py`). New `pipe_settings['max_queued_jobs']`; `max_attempts` also bounds array submissions.

## Design

- Allowance discovery is best-effort: when the scheduler cannot be queried or reports no limit it yields `None` and the array keeps its natural size. `pipe_settings['max_queued_jobs']` states the limit explicitly instead of reading it.
- Sizing is adaptive: whatever the allowance says, an array the queue refuses is halved. Workers claim tasks until none remain, so a smaller array still completes every task.
- Waiting for the queue happens only when even a one-worker array is refused.
- A failed array is retried a bounded number of times, spread in time rather than back to back, and then its tasks become ordinary Scheduler jobs, so a batch always progresses.

## Reuse

Searched for existing submission-cap handling, pipe task ejection, pipe registry cleanup and task-state reading before writing new code. Reused: the cap-message detection `_submission_cap_reached` (shared by `submit_job` and the pipe sizing path, no new patterns), `PipeCoordinator._eject_to_scheduler` (the path that already hands pipe tasks to `Scheduler.run_job`), `_forget_pipe`, `read_task_state` with the guard `ingest_pipe_results` uses, and `pipe_settings['max_attempts']`. Nothing in the repository read a scheduler's per-user job limit, so `arc/job/pipe/queue_limit.py` is new.

## Tests

Run serially, one file at a time:

| File | Passed |
|---|---|
| `arc/job/local_test.py` | 15 |
| `arc/job/ssh_test.py` | 94 |
| `arc/job/pipe/queue_limit_test.py` | 24 |
| `arc/job/pipe/pipe_run_test.py` | 76 |
| `arc/job/pipe/pipe_coordinator_test.py` | 56 |
| `arc/scheduler_pipe_test.py` | 97 |

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3d7c5524d00`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
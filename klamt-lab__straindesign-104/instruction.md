# Issue

**Title:** Release workflow: build the Anaconda package in a job of its own, with Micromamba

## Description

## Problem
`ubuntu-latest` moved to Ubuntu 26.04, whose image ships no conda. The 1.19.2 release stopped at `conda: command not found`, after PyPI and the GitHub release had gone through, so the `cnapy` channel did not get the package. Dispatching the workflow again is no way out, because it would push another commit to `main` and then fail at PyPI, which rejects a version it already has.

## Change
- The Anaconda build and upload move to a separate job, `conda`, which runs after `deploy`. If only this job fails, "Re-run failed jobs" repeats it without touching PyPI.
- `conda-build` and `anaconda-client` come from `setup-micromamba`, as in `CI-test.yml`, whose Linux conda checks pass on `ubuntu-latest`. The hardcoded `/usr/share/miniconda` path is gone.
- The job checks out the tag `v<version>`, since the commit the workflow was dispatched on predates the version bump.
- The job has read-only repository permissions.
- The `conda config --set anaconda_upload yes` line and the final clean-up are dropped. The first ran after the build and had no effect, and runners are discarded after each job.

## Testing
`actionlint` reports nothing. The new job can only really run at the next release, because it needs a dispatch from `main` and the `ANACONDA_API_TOKEN` secret. The conda checks of `CI-test.yml` cover the recipe on every PR, and a local build of `v1.19.2` is being used to upload that version by hand.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71439045c2d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
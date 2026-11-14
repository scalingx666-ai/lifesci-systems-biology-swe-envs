# Issue

**Title:** Add a codecov.yml so the project coverage status tolerates ordinary drift

## Description

## What

Adds a `codecov.yml` (23 lines, no code change):

- `coverage.status.project.default.threshold: 1%`
- `coverage.status.patch.default.target: 80%`

## Why

ARC has no Codecov configuration at all — `.coveragerc` configures coverage.py's *collection*, not
Codecov's *status checks*. With no config, Codecov falls back to its built-in defaults, under which
the `project` status is `target: auto` with a **0% threshold**: total coverage may never dip by any
amount relative to the base commit.

The consequence is that nearly every PR adding code covered below the repository average (~67%)
reports a failing check while every test job, CodeQL and the functional suite are green. Observed
on the current open set, all red on `codecov/project` alone:

| PR | status |
|---|---|
| #653 | `67.03% (-0.10%)` → `67.05% (-0.08%)` after adding a genuine unit test |
| #860, #1016, #1039, #1050, #1054, #1055, #1056, #1057 | red on `codecov/project`, everything else green |

On #653, `codecov/patch` simultaneously reported *"Coverage not affected"* — the gate that actually
judges whether the PR's new code is tested was already satisfied. A check that fails on
one-tenth of a percentage point trains reviewers to ignore it, which costs us the patch signal too.

## What this does and does not change

- **Does:** lets total coverage drift up to 1% without failing the status.
- **Does:** keep an explicit `patch` target, so the coverage of a PR's own new or changed lines
  remains a gating signal. This is the stricter half of the config, not a loosening.
- **Does not:** touch any test or source file, change `.coveragerc`, or alter what coverage is
  collected.
- **Does not:** raise ARC's actual coverage. That is a separate and much larger piece of work.

Note that Codecov re-evaluates statuses on new uploads, so already-open PRs will pick this up on
their next CI run rather than retroactively.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7c2666b19a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** dyngen 1.0.3

## Description

* BUG FIX `generate_experiment()`: Return timepoint groups for `experiment_synchronised()`.

* BUG FIX unit tests: loosen generate partitions constraints.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d08b2ebbfe0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
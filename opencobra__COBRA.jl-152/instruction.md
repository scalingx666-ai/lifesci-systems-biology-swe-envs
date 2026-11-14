# Issue

**Title:** CompatHelper: bump compat for "CPLEX" to "1.0"

## Description

This pull request changes the compat entry for the `CPLEX` package from `0.9` to `0.9, 1.0`.

This keeps the compat entries for earlier versions.

Note: I have not tested your package with this new compat entry. It is your responsibility to make sure that your package tests pass before you merge this pull request.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f255fa99dc5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
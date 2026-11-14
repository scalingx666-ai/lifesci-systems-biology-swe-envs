# Issue

**Title:** Update github action

## Description

As this is the most recent workflow version from https://github.com/r-lib/actions/blob/v2/examples/check-standard.yaml

I added working-directory to setup-r-dependencies and check-package to account for the package code not being in the top level directory.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7a35f639e2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
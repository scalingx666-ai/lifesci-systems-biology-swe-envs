# Issue

**Title:** Version 1.2.11

## Description

Fixes the installers such that GLPK and SCIP are always installed (on some systems, their usage with optlang/cobak is somehow not recognized?), and also the issue #577 thanks to @PyLaRi24

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1700b928cedf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
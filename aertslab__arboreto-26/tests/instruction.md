# Issue

**Title:** Update algo.py

## Description

In the pandas 0.25.3 and later version, the method of DataFrames, "as_matrix()", has been removed. And the substitution of the method is "to_numpy()".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ff7b6f987b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
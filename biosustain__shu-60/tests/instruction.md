# Issue

**Title:** [FIX(ggshu)] Bump dependencies of python package

## Description

This PR relaxes the `numpy` constraint and upgrades `pandas` and python so that **ggshu** can be built for python 3.13.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b389109a07b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
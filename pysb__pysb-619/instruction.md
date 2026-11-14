# Issue

**Title:** Allow Python 3.10 compatibility

## Description

Following up on  this PR
- Removes the networkx minimum version
- Adds pydot as an optional dependency
- Adds Python 3.10 to supported and tested versions

This is helpful for several downstream packages we maintain where we don't want to drop 3.10 compatibility yet.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48b61d8a6cfd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
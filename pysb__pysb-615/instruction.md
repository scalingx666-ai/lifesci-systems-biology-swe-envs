# Issue

**Title:** chore(deps): replace mock with unittest.mock, drop unused deps

## Description

* Replace mock with unittest.mock
* Remove coveralls (CI uses codecov)
* Add note that cythonize requires setuptools

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b4ba3eac459`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
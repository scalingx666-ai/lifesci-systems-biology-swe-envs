# Issue

**Title:** More fixes for when zlib is only static.

## Description

CMake's 'FindZLIB' doesn't account for the situation where zlib is only static, so we have to have some workarounds for if it is.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac1663574354`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
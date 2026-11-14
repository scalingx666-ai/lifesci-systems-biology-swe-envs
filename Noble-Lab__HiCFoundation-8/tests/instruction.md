# Issue

**Title:** Fix symmetric masking and diagonal unit

## Description

Changed the return_diag from unit of pixel into unit of patches, to be compatable with codes after dataloading.
Fix a bug in getting the symmetric mask when the HiC diagonal is a sub-diagonal in the window.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f77452a63419`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
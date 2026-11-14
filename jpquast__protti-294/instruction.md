# Issue

**Title:** Features/extend aa score

## Description

- Added method selection to the aa_score calculations (now user can select between existing "multiplicative" (now set to be default method if not specified) and new "additive" method.
- Added min-max normalization to the aa_score. An additonal column will be cratead in the results df with normalized scores, non-normalized scores are still exported using the expected column name

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa9c9d8ca8e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Fix .set colorby

## Description

The single & at line [393 of 'utils.R'](https://github.com/bioFAM/MOFA2/blob/e605bf285bfa3ed98b3ebfb3b2e9d2b7a68c2717/R/utils.R#L393) and at line [604 of 'plot_weigths.R'](https://github.com/bioFAM/MOFA2/blob/e605bf285bfa3ed98b3ebfb3b2e9d2b7a68c2717/R/plot_weights.R#L604) was preventing the use of a character vector for the argument `color_by` since it wouldn't stop even if the length was greater than 1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e605bf285bfa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Remove mmcs option for generate_steady_states_no_multiphase and fix a warning

## Description

This PR remove obsolete functionality and a deprecated warning. 

First, eb2582205bae8fa9211f5cc19f92d6d85850bae3 eliminates the MMCS option from both `apply_sampling` and `generate_steady_states_no_multiphase`, simplifying the sampling interface and avoiding unsupported paths. The choice of mmcs is not relevant for  `apply_sampling` since the latter accepts a matrix of samples of fixed/known size while mmcs based on given ess generates a variable length matrix of samples. 

Second, a4236f168895347ef571787c1eb5d2765c6abdc8 removes a deprecated warning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cdcb43c888b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
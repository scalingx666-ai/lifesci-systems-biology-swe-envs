# Issue

**Title:** multi-threaded FVA using highspy

## Description

Always use multi-threaded FVA with highspy as solver under Windows and for the other OSes when neither Gurobi nor CPLEX is set as cobrapy solver.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c3000eae78d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
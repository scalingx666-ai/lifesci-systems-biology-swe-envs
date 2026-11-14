# Issue

**Title:** pyPESTO v0.8.0

## Description

- **Only to be released after merging in #1804 and #1797**
- Bumped up amici version to most recent

## CHANGELOG

- Breaking changes
    - Remove deprecated ``PetabImporterRR``; use ``PetabImporter(..., simulator_type="roadrunner")`` (#1793)
    - Raise minimum versions of numpy, scipy, pandas, matplotlib, amici (>=1.2) and other optional extras (#1797)
    - Gradients of parameters without sensitivities are NaN instead of 0 (#1776)
- PEtab v2 (experimental)
    - Hierarchical optimization for PEtab v2 problems (#1740, #1744)
    - ``parameter_scales`` argument for log-scale estimation (#1782)
- Hierarchical optimization
    - Fix wrong results for observables with constant offset terms (#1786)
    - Respect noise models of data without inner parameters (#1778, #1779)
    - Fix ``NumericalInnerSolver`` stopping early for small sigmas (#1788)
    - Plot observable mappings of offset-only relative observables (#1787)
- Other smaller Bugfixes (#1798, #1804, #1759, #1768)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c2a45072a1e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
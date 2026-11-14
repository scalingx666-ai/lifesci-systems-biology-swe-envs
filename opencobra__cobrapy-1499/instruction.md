# Issue

**Title:** fix: handle empty internal selections in loopless analysis

## Description

The default Fast-SNP `add_loopless` raises an `IndexError` on a feasible acyclic pathway: the finder returns no cyclic internal reactions, then `np.array([])` is used as a floating-point index. `find_cyclic_reactions` has the same failure on boundary-only models, also affecting loopless FVA.

Two early returns handle empty internal selections. Existing method/cutoff/stop-count validation remains before the guards. The documented cycle constraint is vacuous on an empty selection.

- [x] Description of fix
- [x] Regression cases for acyclic/boundary-only/all-blocked models, empty selections under both formulations, the finder and downstream FVA/full flux vectors
- [x] Next Release entry

Validation on frozen devel `a9c5ced29670bed5035fb19e87e7b0b588adb62d`, Python 3.11 / GLPK:

- 16 new parameter cases: **15 failed / 1 passed** before the patch.
- Three related nonbenchmark/nonparallel suites: **37 passed, 9 deselected** after the patch.
- Separate independent diamond-network, forced-cycle, subset/iterable/context/user-constraint and FVA checks: baseline **24 failed / 23 passed**, candidate **47 passed**. Every baseline failure is the empty-index exception.
- Black 25.1.0, isort 6.0.1, flake8 7.1.2 with docstrings/bugbear, and diff whitespace checks passed on changed files.

The independent diamond has arm capacities 3/7 plus a first-arm cap 2, giving optimum 9. At half optimum, supply/drain ranges are [4.5,9], first-arm reactions [0,2], second-arm reactions [2.5,7]. Both FVA algorithms and full flux distributions are checked against these analytic bounds.

The inspected #1472 branch retains both empty-index paths; this is a separate edge-case repair. The full solver/platform matrix and benchmark suite were not run locally. GLPK is the tested backend.

Prepared with AI assistance for discovery, implementation and independent checking. This is a software correctness contribution; maintainer review is requested.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fdbcc96fde1e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
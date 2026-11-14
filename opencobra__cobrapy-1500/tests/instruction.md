# Issue

**Title:** fix: orient FASTCC constraints for negative-only reactions

## Description

FASTCC constructs `v >= z >= 0` for every irreversible reaction, although COBRApy also permits irreversible reactions with negative-only bounds. A feasible source–transfer–drain pathway whose reactions are reversed and bounded by `[-10, -1]` can therefore make the artificial consistency LP infeasible. Its exact mass-balance witness is `(-7, -7, -7)`. Zero-inclusive negative bounds can also produce false negatives, depending on the solve path.

Use `-v` in the auxiliary inequality when a reaction's upper bound is nonpositive. Original stoichiometry, bounds and objective are preserved. This is direction normalization for the existing FASTCC API; it does not change the published algorithm's nonnegative irreversible convention.

Validation on GLPK:

- 25 added cases cover all eight pathway orientations with open, closed and forced-minimum bounds, blocked/fixed-zero reactions, a reversible cycle and input context restoration.
- The FASTCC module reports 28 passed, 2 deselected. Benchmark/large-model tests and alternate solvers were not run locally.
- An independent five-case suite reports 1 failed / 4 passed before this patch and 5 passed afterward; the stable failure is the strictly negative pathway above. Exact rational mass balance independently establishes the expected reaction set.
- Black 25.1.0, isort 6.0.1 and flake8 7.1.2 with docstring/bugbear checks pass. A release note is included.

Related work: #1428 is already incorporated in the tested development source. #1495 includes negative-only pathway coverage in its new `spectra_cc` sibling and discusses FASTCC false negatives, but does not modify `fastcc.py`. This patch credits that prior coverage and applies the normalization to the existing API; it claims neither a new algorithm nor first discovery of negative-flux handling.

The coordinate-equivalence argument concerns `Sv=0` and box bounds; any additional flux constraints must be transformed too. AI assisted implementation and a separate skeptical review; maintainer confirmation is requested.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b55b24e4b022`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
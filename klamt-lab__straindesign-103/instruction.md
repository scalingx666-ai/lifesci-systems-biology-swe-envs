# Issue

**Title:** Assemble exact kernels from the nonzeros of the RREF

## Description

## Problem
`_nullspace_sparse` reads the kernel off the RREF by visiting every (free column, pivot row). The RREF is very sparse, so nearly all of these lookups find nothing. On iAF1260b the seven nullspaces of one run took about 664 million dictionary lookups.

## Change
- Collect each kernel column's entries from the nonzeros of the RREF rows, so the cost follows the fill. The kernel and the order of its entries are unchanged.
- `to_sparse_pattern` raised `AttributeError` on a matrix without sparse storage, such as the empty kernel of a matrix with full column rank. It now returns an empty pattern.

## Effect
Measured through Kimonu on the 33 genome-scale kinetic benchmark models, one core, median of three runs, on shared nodes (so the timings are noisy):

| | Before | After |
|---|---|---|
| iAF1260b | 104 s | 22 s |
| iS_1188 | 51 s | 16 s |
| iSDY_1059 | 42 s | 20 s |
| Slowest single run of the 33 models | | 22.4 s |

Those runs used an equivalent patch applied at run time, and their results were identical on all 99 runs. Any other caller of the exact nullspace uses the same code path, but I did not measure compression or strain design separately.

## Tests
- New in `tests/test_07_compression.py`: the kernel against a reference that visits every pair, in int64 and big-integer storage, and `to_sparse_pattern` on an empty kernel.
- The `--medium` and `--large` suites are being run locally on a compute node, since `--large` does not run in CI. Results will follow in a comment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10a81e7323ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
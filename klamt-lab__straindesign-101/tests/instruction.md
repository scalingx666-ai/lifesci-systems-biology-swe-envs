# Issue

**Title:** Faster preprocessing: sparse kernel edits, bulk GPR detach, FVA probe, parallel reversibility

## Description

## Summary

Faster preprocessing for strain design, with identical results: compression, FVA dispatch, the reversibility scan and the worker pool. This is one of three PRs split from #95, and it is independent of the other two (#100, #102).

**Compression**
- RationalMatrix batch edits collect in a per-column store and are written back once at `end_batch_edit`. Before, every edit was an element-wise LIL write followed by a CSC conversion per column operation. `add_scaled_column` and `scale_column` open a batch themselves when called outside one.
- GPRs are detached in bulk (`_detach_gprs`) instead of going through the cobra setter (a parse, a GPR copy and gene relinking) per reaction. That setter path ran ~78k times per `compress_model` on Recon3D. A reaction whose rule comes out of compression unchanged gets its GPR object back.
- `_rename_lumped` uses a reverse map, and `compress_model_parallel` no longer allocates a dense old-by-new matrix it never read.
- The rational arithmetic is unchanged: preprocessed e_coli_core and iML1515 models are identical to main's.

**FVA (`speedy_fva`)**
- Phase 2 hands its objectives to the worker pool from 500 remaining objectives on (main: 4000), but first runs sequentially as a probe (50 LPs or 0.5 s). It hands over the rest only when their projected sequential time exceeds the pool's start-up, about 2 s plus 0.07 s per worker. A count alone cannot decide this: an LP of a 472-reaction network solves in under a millisecond, while the pool takes seconds to start. With the threshold at 500 but no probe, one FVA on the iMM904 mcs network took 6.85 s pooled against 0.49 s with the probe; bounds agree within 7e-8 relative.
- The phase-1 scan runs by default only when phase 2 stays sequential: against pooled LPs, its own full-model LPs cost more than the objectives they remove (Recon3D: folded FVA 15.9 to 7.1 s).
- GLPK always scans and never pools. Its warm-started dual simplex can stall on objectives the scan settles, and its pool worker rebuilds the LP for every objective. This was pre-existing on main.

**`fast_reversibility`** can run on a worker pool from 1000 reactions on. Like FVA's phase 2, it first solves sequentially as a probe and hands the remaining directions to the pool only when their projected sequential time exceeds the pool's start-up. The pool works in rounds, and each round's flux vectors certify directions before the next round is formed. The per-direction decisions are the same as the sequential scan's. Recon3D: 135 s on main, 11 s here; iML1515 stays sequential.

**`SDPool`** passes initargs through a pickle file on every platform, not only Windows. A large payload written to a spawned worker's pipe blocks the parent until that worker has started, so workers started one after another (~1.5 s each).

## Benchmarks

Preprocessing time (start of `compute_strain_designs` to the MILP construction), main vs this branch, CPLEX, same node: (e210, seed 1, best of the repetitions)

| network | main | this PR | |
|---|---|---|---|
| iML1515 (gene) | 10.5 s | 6.2 s | 1.7x |
| iJN1463 (gene) | 10.4 s | 5.6 s | 1.9x |
| yeast8 (gene) | 28.8 s | 22.0 s | 1.3x |
| HumanGEM media (gene) | 590.0 s | 81.8 s | 7.2x |
| Recon3D (gene) | 302.7 s | 64.2 s | 4.7x |
| HumanGEM raw (gene) | 355.3 s | 63.8 s | 5.6x |
| iMM904 mcs, problem 1 | 3.0 s | 2.4 s | 1.2x |
| iJO1366 mcs, problem 1 | 8.4 s | 8.0 s | 1.1x |
| iJM658 mcs, problem 1 | 1.0 s | 1.0 s | 1.0x |

## Tests

`test_02`: dispatch tests for FVA and the reversibility scan (a small network stays sequential; the hand-off reaches the pool and returns the sequential result, CPLEX/Gurobi only). Local full suite (CPLEX, Gurobi, GLPK, SCIP): 438 passed, 7 skipped; CI green.

## Interactions

Touches `compression.py`, `speedy_fva.py`, `lptools.py` and `pool.py` only. It merges cleanly with #92/#93/#94, #89, #100 and #102 in any order.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RFtof9nZXFvCNoXz19po8C

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `254122d9ad8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
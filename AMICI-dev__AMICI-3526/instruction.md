# Issue

**Title:** Read ReturnDataView/ExpDataView field shapes on first access

## Description

Stacked on

`ReturnDataView.__init__` built a dict with the shapes of all array fields. For every view, that read about 35 attributes of the SWIG-wrapped `ReturnData` and allocated about 40 GC-tracked objects, whether or not any field was read. `ExpDataView` did the same for its fields.

`_field_dimensions` is now a class attribute that maps each field to a function of the wrapped object returning the field's shape. It is evaluated when the field is first accessed, and the resulting array is cached as before. Constructing a view is now just a type check plus setting the pointer and an empty cache.

Shapes are now read at the first access of a field rather than at view creation. So an `ExpDataView` sees changes to the `ExpData` made before a field is first read; before, this failed with a reshape error. A new test covers this.

## Measurements

Setup: Python 3.13, a 2-state model, `run_simulations` with 9169 `ExpData`s and forward sensitivities, 6 calls (55k views). Afterwards `llh`, `sllh` and `FIM` are read from every result.

| | view construction | GC time | gen0 collections | reading `llh`, `sllh`, `FIM` |
|---|---|---|---|---|
| #3525 | 1.36 s | 0.44 s | 1049 | 0.32 s |
| this PR | 0.03 s | 0.01 s | 77 | 0.31 s |

With 12M long-lived GC-tracked objects in the process (standing in for a large PEtab problem), view construction went from 2.29 s to 0.03 s, and GC time from 1.32 s to 0.82 s. One full collection remains, triggered by the earlier allocations of the large heap.

This is the cost that the profile in  charged to `XArrayFactory.__init__` (about 11 s for 18,338 views).  for why cProfile charged it there.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `76e46ab5aa3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
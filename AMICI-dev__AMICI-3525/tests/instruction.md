# Issue

**Title:** Break the ReturnDataView <-> XArrayFactory reference cycle

## Description

Stacked on

`ReturnDataView.__init__` stored `XArrayFactory(self)` as `self.xr`, and the factory holds a reference back to the view. Because of this cycle, a `ReturnDataView` and the C++ `ReturnData` it owns were never freed by reference counting, only by the cyclic garbage collector.

This PR makes `xr` a property that creates the factory on access. `ReturnDataView.__dir__` still lists `xr`. A new test checks that a view and its `ReturnData` are freed with the GC disabled; it fails without this change.

## Measurements

Investigated after the profile in  where 18,338 `ReturnDataView`s took about 11 s, all charged to `XArrayFactory.__init__`. Setup: Python 3.13, a 2-state model, `run_simulations` with 9169 `ExpData`s and forward sensitivities, and 4M dicts (12M GC-tracked objects) kept alive to stand in for a large PEtab problem.

**Memory (the cycle matters).** Results that a caller drops after reading `llh` stay alive. While `run_simulations`' result list is in use, they move into the oldest GC generation, so they are freed only at the next full collection. Over 20 calls (200 time points):

| | `ReturnData`s alive after a call (max) | peak RSS |
|---|---|---|
| with cycle (`main`) | 54,250 (about 6 calls' worth) | 3.7 GB |
| this PR | 0 | 2.3 GB |

The larger the heap, the rarer full collections are (CPython runs one only when the objects promoted since the last one exceed 25% of the old generation), so more results pile up.

**Time (the cycle is not the cause of the 11 s).**
- Each `ReturnDataView` makes 40 GC-tracked allocations, mostly the `_field_dimensions` dict of lists. Those allocations trigger the collections. Since Python 3.12, a collection runs at the next eval-breaker check, which is the entry of `XArrayFactory.__init__`. So cProfile charges the collection to that function, including full collections of the whole heap. With this PR the same collections are charged to `SwigPtrView.__init__` instead.
- Breaking the cycle saves little GC time: 0.81 s → 0.66 s for 55k views (6 calls, 3 time points). Full collections happen as often as before.
- The 11 s in the profile fits one or more full collections of a large heap (here about 0.6 s per full collection of 12M objects). This PR does not remove those.

## Not in this PR

Most of the remaining construction cost is the eager `_field_dimensions`: about 35 SWIG attribute reads (about 30 µs per view) and 40 tracked allocations. In a quick emulation, computing dimensions lazily on first field access cut construction from 2.44 s to 0.02 s for 55k views, and gen0 collections from 1054 to 76. Done in

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `739b88c822c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
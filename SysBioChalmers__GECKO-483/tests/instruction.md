# Issue

**Title:** tutorials: regenerate full_ecModel ecYeastGEM.yml with GECKO 4 and RAVEN 3

## Description

Regenerates `tutorials/full_ecModel/models/ecYeastGEM.yml`, the ecModel distributed with the tutorial, now that #481, #482 and SysBioChalmers/RAVEN#751 are merged. This was left out of #481 because RAVEN 3.0.0b1's YAML writer produced a file that YAML parsers could not read.

**Before:** built with the GECKO 3 pipeline, with protein pool and enzyme usage reactions in the GECKO 3 reverse direction. GECKO and geckopy flip it on load, and geckopy warns about this.

**After:** the STEP 52 model from `protocol.m` on `develop4` with RAVEN `develop3`. It is in the GECKO 4 forward-direction format, includes the sensitivity-tuned kcats and the r_0079 curation, and has properly nested `ec-rxns` enzyme entries.

## Checks

- `protocol.m` runs end to end (28 min, MATLAB 2024b, Gurobi 13.0.1) and reloads this file at STEP 66.
- geckopy (`develop`, with SysBioChalmers/geckopy#54) loads it with no warnings: 8001 reactions, 4834 `ec.rxns`, 1144 enzymes, all usage reactions and the pool in the forward direction. Maximum growth is 0.4391 /hour, identical to MATLAB at STEP 69-70.
- The other tutorial outputs came out identical to those committed in #481 (`ecFVA.tsv` value by value; the PDFs differ only in their embedded timestamps), so they are not part of this PR.

Once merged, `develop4` is ready for the `v4.0.0b1` tag.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d415d7f5f183`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
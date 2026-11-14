# Issue

**Title:** Let the BRENDA aggregation be chosen

## Description

### Description

`kcat.tsv` and `sa.tsv` each record a maximum **and** a median per (EC, substrate, organism) triple, but `loadBRENDAdata` read the maximum with no way to ask for the other — as `databases/README.md` noted. geckopy, which produces these files, lets a project choose between them; this brings GECKO in line.

- `params.kcatAggregation` on the model adapter sets it for a project.
- `'kcatAggregation'` as a name-value argument to `fuzzyKcatMatching` or `loadBRENDAdata` sets it per call.
- The default is `'max'`, unchanged.

Both aggregation layers switch together, as they do in geckopy: the column read from the file, and the collapse of the entries matched at one search level. Which triple is matched, at which wildcard level and origin, is untouched — only the value taken from it changes.

### Argument validators

New, and the reason is worth stating. Mixing positional and name-value arguments puts an argument *name* into a positional slot: `fuzzyKcatMatching(model, [], adapter, 'kcatAggregation', 'median')` assigns `forceWClvl = 'kcatAggregation'`, and `while forceWClvl > 0` on a char array is all-true, so every EC number was silently wildcarded and the run completed with wrong values. The validators reject it, and a test covers it. The name-value form `fuzzyKcatMatching(model, 'ecRxns', [], 'modelAdapter', adapter, 'kcatAggregation', 'median')` is the supported way to mix.

### Testing

`geckoCoreFunctionTests` run locally on MATLAB R2024b with RAVEN 3.0.0b1: **51 passed / 60**, against a **50 / 59** baseline on the current `develop4` — the same nine pre-existing failures, plus the new test. The fixture `kcat.tsv` now records a median that differs from its max (the max column is unchanged), so the new test can tell the two apart; it checks that the values follow the chosen column while the matching itself does not move.

### I hereby confirm that I have:
- [x] Tested my code on my own computer for running the model
- [x] Selected `develop4` as a target branch
- [x] Any removed files have been removed from the repository

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbc4ca3311df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
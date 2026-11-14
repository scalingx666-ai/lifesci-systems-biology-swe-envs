# Issue

**Title:** fix: prefix whole gene ids in grRules in addIdentifierPrefix

## Description

### Main improvements in this PR:
- fix:
  - `addIdentifierPrefix`: a gene id containing a dash, dot or colon (for example the fly gene `5-HT1A`) got a `G_` prefix at every word start in `grRules` (`G_5-G_HT1A`) but one prefix in `model.genes` (`G_5-HT1A`). `exportModel` then failed in `checkModelStruct` because the grRules named genes that were not in `model.genes`. Genes are now prefixed as whole tokens, leaving `and`, `or` and brackets alone.
- tests:
  - `tConversion`: a gene with a dash and one with a colon keep one prefix and still match `model.genes`.

Found when exporting the regenerated Fruitfly-GEM to SBML (SysBioChalmers/Human-GEM#1141). The full `testing/function_tests` suite passes (MATLAB R2024b, Gurobi).

#### Instructions on merging this PR:
- [X] This PR has `develop3` as target branch, and will be resolved with a *squash-merge*.
- [ ] This PR has `main` as target branch, and will be resolved as descriped [here](https://github.com/SysBioChalmers/RAVEN/wiki/Development-policy#make-a-new-release).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `083dccc96f95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
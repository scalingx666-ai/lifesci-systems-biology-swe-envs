# Issue

**Title:** [FIX] Make `gene_reaction_rule` reaction fields optional in map JSON files

## Description

(maybe.)

### Description

Escher may not include `gene_reaction_rule` in the map, and **shu** was strict in that field being present, which is a mismatch in the spec.

### Implementation

`shu::escher::Reaction::gene_reaction_rule` was wrapped in an `Option` and a little test was added.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd1ae9b426ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
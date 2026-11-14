# Issue

**Title:** wrapper around UMAP + small top_features fix

## Description

This Pull request adds a wrapper around `scanpy` UMAP that
- compute neighbours (if not present) using the MOWGLI weight matrix
- compute UMAP using default `scanpy` implementation
- plot UMAPs using the canonical `sc.pl.umap` for one or more factors computed by Mowglu.

Moreover, it adds two small modifications to the top_features() method, namely:
1. return the `ax`, to the output of `top_features` into matplotlib subplots
2. enables`top_features` to accept custom color palettes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `160e714a64f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
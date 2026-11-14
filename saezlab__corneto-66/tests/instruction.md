# Issue

**Title:** Release 1.0.0rc9: shortest-path fixes and biological signaling plots

## Description

Prepare CORNETO 1.0.0rc9 with corrected shortest-path flows and the opt-in biological signaling plotting preset.

Shortest paths now respect directed and undirected traversal, charge magnitude costs, and extract one optimal path from tied fractional LP flows without an automatic integer solve. Multi-condition models handle reverse traversal, one condition, and shared-edge L0 selection. PICOS objective construction and missing-solution handling are corrected.

The `signaling_biology` plotting preset adds explicit receptor/regulator annotations, activity colors, and interaction arrowheads. RC9 release notes describe the compatibility changes: shortest-path construction defaults to an LP, costs must be finite and nonnegative, and hyperedges are rejected.

Validation:
- Full clean-snapshot suite: 1,061 passed, 34 skipped.
- Repository-wide Ruff lint and formatting checks, Poetry metadata checks, and distribution checks passed.
- Full Sphinx build with notebook execution and warnings treated as errors passed.
- Publication history and complete diff reviewed; no private research, credentials, datasets, or unrelated uncommitted edits included.

The release tag is created separately after this PR passes CI, merges, and the release dry run is reviewed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9f6d238d6c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
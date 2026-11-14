# Issue

**Title:** Optimize sqlite ontology build size

## Description

This PR makes improvements to the sqlite ontology backend to significantly decrease the size making it a better fit for Dockerized deployments. The changes are
- Remove redundant indexes that are already created via UNIQUE
- Compress child_lookup/parent_lookup values since these are often long lists of nodes
- Remove redundant relationships table
- Fix name lookup and isa_partof checking
- Add a vacuum at the end of the build

This decreases the .db's size from ~3.3 GB to ~710MB without a negative effect on performance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6dfd239e0dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
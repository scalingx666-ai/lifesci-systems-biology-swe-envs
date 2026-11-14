# Issue

**Title:** Look-up survives ChEMBL failing

## Description

On the live site the look-up failed outright ("Failed to fetch") when ChEMBL returned HTTP 500 — an error page without a CORS header, which the browser reports as blocked. ChEMBL's whole API then went down (status page included).

- three tries per request, 1.2 s then 3 s apart
- direct InChIKey look-up rather than the filter query
- a ChEMBL failure no longer sinks the look-up: structure, properties and library match still show, with "ChEMBL did not answer — try again"

Tested in headless Chrome during the outage: every path behaves; the only console errors are ChEMBL's own failed requests.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9353c9ee702c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
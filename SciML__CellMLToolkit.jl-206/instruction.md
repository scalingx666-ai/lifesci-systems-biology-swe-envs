# Issue

**Title:** Require Symbolics 7.39.2 (32-bit hasha_seed)

## Description

## Summary
Force Symbolics ≥7.39.2 so x86 resolves SymbolicUtils ≥4.46.4 (hasha_seed).

## Test plan
- [ ] x86 Core green

Made with [Cursor](https://cursor.com)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4049afacc56`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
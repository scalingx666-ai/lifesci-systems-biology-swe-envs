# Issue

**Title:** Allow Catalyst 17

## Description

Catalyst 17.0.0 is released (SciML/Catalyst.jl#1572). It updates to JumpProcesses 10, whose breaking changes concern jump problems and RNGs. MomentClosure does not use the changed APIs, so this PR widens the Catalyst compat and keeps Catalyst 16 support.

## Changes
- `Catalyst = "16.2"` → `"16.2, 17"`.
- The JumpProcesses compat (`"9.29, 10.0"`) already admits JumpProcesses 10. The docs' `SSAStepper` ensemble solves pass no `rng` to `JumpProblem`, so they work unchanged.

A separate commit bumps the version to 0.4.9 for a patch release. Drop it if you would rather bump the version in its own PR.

## Validation
Run locally on Julia 1.12.7 with 4 threads: the Core test group passes with Catalyst 16.5.0 and 17.0.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code) 2.1.310 (model: claude-opus-5-5)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4bbb1fb2da2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
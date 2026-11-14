# Issue

**Title:** Add AirspeedVelocity benchmarking CI

## Description

## Summary

- Adds `.github/workflows/benchmark.yml` running AirspeedVelocity on pull requests (Julia `1` and `lts`, 30 min timeout), following the OrdinaryDiffEq.jl setup.
- Adds `benchmark/benchmarks.jl` with a small `SUITE` covering representative workloads for this package.

The suite was verified locally in a fresh environment: it loads and all benchmarks run in ~31s.

#### Test plan

- [x] `run(SUITE)` locally: all benchmarks pass (~31s)
- [x] Runic formatting clean on `benchmark/benchmarks.jl`
- [ ] \"Benchmark this PR\" workflow triggers and completes on this PR

🤖 Generated with [Devin](https://devin.ai) (harness: devin 3000.10.21, model: SWE-2 Max)
Session: local transcript /home/crackauc/.local/share/devin/cli/summaries/history_ccb52064e6514b21.md

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc576ef0fe02`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Update PEtab benchmark collection repository location

## Description

The PEtab benchmark collection moved from `Benchmarking-Initiative/Benchmark-Models-PEtab` to `PEtab-dev/petab-benchmark-problems`, and its default branch is now `main` instead of `master`. Installing `benchmark_models_petab` from `@master` fails, which breaks the benchmark collection workflows (e.g., https://github.com/dweindl/AMICI/actions/runs/42625199752/job/129187050198).

This updates the dependency group in `pyproject.toml`, `doc/rtd_requirements.txt`, the binder Dockerfile, example notebooks, and links in test comments.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adfd4b296e71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
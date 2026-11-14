# Issue

**Title:** GHA fix for CI

## Description

`ubuntu-latest` now resolves to Ubuntu 26.04, which no longer ships
`libatlas-base-dev`. The apt install of the AMICI build dependencies
therefore failed, and with it every job that builds AMICI (base,
hierarchical, select, notebooks, docs). Replace ATLAS with
`libopenblas-dev`, as AMICI itself did when moving its CI to
Ubuntu 26.04 (AMICI-dev/AMICI#3434).

Also drop `coinor-libipopt1v5`, which does not exist on 26.04;
`coinor-libipopt-dev` pulls in the matching runtime library.

Run `install_deps.sh` with `set -e`, so a missing apt package fails the
step right away instead of surfacing later as a misleading error
(e.g. AMICI built without HDF5).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `98cf21e10120`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
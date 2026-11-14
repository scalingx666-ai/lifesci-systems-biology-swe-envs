# Issue

**Title:** chore(codecov): only enforce on patch, not project

## Description

codecov provides two github actions checks, project and patch. Patch is the more useful - project's regular failure obscures our main test suite.

Convert the project check to informational only using codecov.yml

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80943191e737`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Add NPM package-lock.json to version control

## Description

"The package-lock.json file needs to be committed to your Git repository, so it can be fetched by other people, if the project is public or you have collaborators, or if you use Git as a source for deployments."
https://nodejs.dev/the-package-lock-json-file

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d60004dff050`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
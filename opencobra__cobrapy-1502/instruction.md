# Issue

**Title:** fix: copy a reaction that already belongs to another model

## Description

* [x] fix #1456
* [x] description of feature/fix
* [x] tests added/passed
* [x] add an entry to the [next release](../release-notes/next-release.md)

Adding a reaction that already belongs to another model used the same object. Changing bounds on the destination also changed the source, and the reaction's model pointer moved.

`add_reactions` now copies a reaction whose model is another model. A reaction that is not yet in a model is still added as the same object. A reaction already in the destination is still ignored.

## Verification

`tox run -e py313,isort,black,flake8 -- --benchmark-skip` on Windows, Python 3.13.1.

py313: 594 passed, 71 skipped, 10 xfailed, 3 failed. `test_groups` and `test_gprs` raise `UnicodeEncodeError` while writing SBML because the test opens the file in the gbk locale. `test_remote_load[BIOMD0000000633]` failed because the BiGG connection failed. isort, black, and flake8 passed.

A free reaction is not copied. A reaction whose model pointer was cleared inside a context looks the same and is still added as the same object. Metabolites and genes that already exist in the destination are still reused by id. Groups are not copied with the reaction.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `013bfda3e082`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
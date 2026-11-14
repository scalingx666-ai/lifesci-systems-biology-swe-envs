# Issue

**Title:** BUGFIX for sparse expression matrices

## Description

Hi,

arboreto seems to nominally support sparse matrices (according to the docs/docstrings),
however I ran into a couple of errors:

- `len()` and `np.delete()` doesn't work on sparse matrices
- `sklearn.ensemble.GradientBoostingRegressor` can handle sparse matrices for `X`,
but `y` has to be dense!

Except for potential memory saving, this unfortunately doesn't speed things up much. Not an expert in boosting, but I don't see how to exploit sparsity for speed in boosting, so that's expected I guess.

Actually sparse matrices slow down `GradientBoostingRegressor` quite a bit.
This seems to be due to some conversions of sparse matrices internally (csc vs csr):
- for arboreto *csc* makes the most sense (since we're pulling out columns all the time)
- `GradientBoostingRegressor` wants *crs*
- but even if one provides a *csr*-matrix to `GradientBoostingRegressor` it does some weird csr->csc conversion internally. Not sure whats going on there.

So maybe it makes the most sense **in the future** to have the original expression matrix sparse, pull out the transcription factor matrix and target gene vector and cast them into dense matrices (the tf-matrix shouldnt be too large either, around 2000 columns)

Let me know what you guys think!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ff7b6f987b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
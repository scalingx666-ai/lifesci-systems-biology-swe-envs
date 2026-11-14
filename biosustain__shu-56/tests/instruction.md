# Issue

**Title:** [FEAT] geom_col

## Description

### Description

Implement `geom_col` for column plots. This is a middle ground between a distribution and a boxpoint, since it is able to plot the value (like the boxpoint) and error bars (both confidence/credibility intervals, quantiles, etc.).

![image](https://github.com/user-attachments/assets/379cd4c8-ab19-40ac-abbc-ef2598fbc311)


### Implementation

* [x] New input data fields. It is allowed to have column data with/without ymin and with/without ymax; plotting the errorbars is optional.
* [x] Box point axes generation is now generic so that specific `Xaxis` are built for columns.
* [x] The histogram legend a color change is reused for columns if present.
* [x] `geom_column` was added to the python API.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e39427484df3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
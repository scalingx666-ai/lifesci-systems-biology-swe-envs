# Issue

**Title:** Add fc_threshold parameter to cnetplot

## Description

## Summary
- Add new `fc_threshold` parameter to `cnetplot.enrichResult` function
- Filters genes to only include those with `|foldChange| > fc_threshold`
- Allows users to plot only high fold-change genes (e.g., `fc_threshold = 1`)

## Usage
```r
cnetplot(x, foldChange = fc, fc_threshold = 1)
```

## Example
**Left:** cnetplot with fc_theshold=NULL (=0) default behaviour plotting all genes for concept. 
**Right:**  cnetplot with fc_threshold=1.5. Plotting only genes with abs(fc)>1.5. The plot is smaller and better readable.

<img width="45%" halt="image" src="https://github.com/user-attachments/assets/e6bdc007-9e7c-43db-9082-36a13ce7cd3a" />
<img width="45%" halt="image" src="https://github.com/user-attachments/assets/fff0a5e1-2c32-474f-a3b4-a6ed20a61518" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5647eb4b7f8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
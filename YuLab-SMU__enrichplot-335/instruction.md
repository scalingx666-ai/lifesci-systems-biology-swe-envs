# Issue

**Title:** Improvements heatplot and treeplot

## Description

**Heatplot**:  

1. Add showTop parameter to limit number of genes shown. Genes are sorted by nfreq*abs(FC) such that most shared and higher absFC genes are preferred.  Upper plot below shows current heatplot with 10 categories and too many genes so axis cannot be read. Bottom plot shows same plot with showTop=100.
2. Set reverse is false to correct color legend. 

```
p1 <- heatplot(obj, foldChange=fc, showCategory=10, showTop=NULL, label_format=120) + tt
p2 <- heatplot(obj, foldChange=fc, showCategory=10, showTop=100, label_format=120) + tt
plot_list(p1, p2, ncol=1, tag_levels='A', tag_size = 44)
```

<img width="3007" height="1213" alt="image" src="https://github.com/user-attachments/assets/3582b56c-d711-4bc1-914c-9cea572e5da8" />

**Treeplot**

1. Add size_par parameter because gseaResult objects do not have Count column but setSize should be used. 
3. Disable log10 transform if color_var is not pvalue/qvalue or p.adjust. If color_var is e.g. NES, we use bluered

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0a81b43a451`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
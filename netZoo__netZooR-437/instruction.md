# Issue

**Title:** Expanded statistics reporting in SEAHORSE for phenotype-phenotype, ph…

## Description

Expanded statistics to include the following:

- LIMMA moderated t-statistic for linear regression on expression data
- t-statistic for linear regression on continuous network features
- z-statistic for logistic regression on dichotomous network features
- p-values for correlation between expression and continuous phenotypic data
- ANOVA F-statistic for association between expression and nominal phenotypic data
- LIMMA moderated t-statistic for association between expression and dichotomous phenotypic data
- p-values for correlation between continuous network features and continuous phenotypic data
- ANOVA F-statistic for association between continuous network features and nominal phenotypic data
- t-statistic for association between continuous network features and dichotomous phenotypic data
- t-statistic for association between dichotomous network features and continuous phenotypic data
- Chi-square statistic for association between dichotomous network features and nominal / dichotomous phenotypic data
- p-values for correlation between continuous phenotypes
- t-statistic for association between continuous and nominal phenotypes
- ANOVA F statistic for association between continuous and dichotomous phenotypes
- Chi-square statistic for association between nominal / dichotomous phenotypes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df65cc1e8aa1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
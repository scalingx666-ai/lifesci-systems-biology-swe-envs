# Issue

**Title:** fix mismatch between label and data in tableGrob2

## Description

修复 gseaplot2 画图时 pvalue_table_rownames 与 pvalue_table_columns 不匹配问题

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41a9f9720994`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
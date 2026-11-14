# Issue

**Title:** Require igraph version >=1.3.0

## Description

Hi,

Thank you for developing this nice set of packages! I recently hit up against a bug when using generate_dataset (more specifically, generate_feature_network), seeing the error message:

```
Error in igraph::bfs(., sample.int(ncol(realnet), 1), mode = "all") : 
  unused argument (mode = "all")
```

I was running igraph v1.2.9. Updating igraph to v1.3.0 fixed this bug. My patch makes the package require at least this version of igraph.

I'm afraid I've not been able to test properly since the process then crashes at a later stage, but I believe that this patch should at least fix the first problem!


Thanks,
George

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e293b604fdf4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
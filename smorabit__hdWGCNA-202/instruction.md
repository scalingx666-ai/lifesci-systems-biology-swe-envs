# Issue

**Title:** Add corSparse Internally (qlcMatrix archived from CRAN)

## Description

Hi Sam/Swarup Lab,

Quick PR here to overcome recent archiving of qlcMatrix package from CRAN.  Given that the package hasn't been updated in 5+ years and has been archived for 1.5 months it appears to be abandoned.  This prevents hdWGCNA installation as it's listed in Imports.  This can be solved by installing from source from CRAN archive but that's not obvious solution for many.

This recently came up as issue for Signac package () and they decided to simply implement function internally () with reference to original stackoverflow post and qlcMatrix package (which did not have any license listed).

This PR simply implements the function the same as Signac did (and now also references Signac's implementation.

Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `952eda63370a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
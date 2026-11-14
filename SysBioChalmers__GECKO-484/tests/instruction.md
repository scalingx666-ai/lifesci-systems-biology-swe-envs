# Issue

**Title:** Divide a BRENDA kcat by the substrate it was measured on

## Description

### Problem

A BRENDA kcat is a turnover per molecule of one named substrate. To use it as a
reaction turnover it has to be divided by that substrate's stoichiometric
coefficient. `matchKcat` divided by the smallest coefficient in the reaction
instead:

```matlab
if ~isempty(subs{k}) && strcmpi(subs{k},KCATcell{2}(indx))
    if KCATcell{4}(indx) > 0
        coeff = min(substrCoeff);
```

Those are the same number only when the reaction happens to be written per the
measured substrate. When another substrate has a coefficient below 1, the
division inflates the kcat rather than reducing it.

### Effect

yeast-GEM writes cytochrome c oxidase (`r_0438`) per one cytochrome c, so its
substrates are ferrocytochrome c at 1.0, H+ at 1.266 and oxygen at 0.25.
BRENDA's *S. cerevisiae* value under EC 7.1.1.9 is 1500/s, and 1500 / 0.25 gives
the 6000/s carried by the `full_ecModel` tutorial model, at wildcard level 0 and
origin 1.

Measured turnover for cytochrome c oxidase is in the low hundreds per second.
The inflated value makes respiration look cheap enough that the electron
transport chain no longer saturates in proteomics-constrained models built on
this ecModel.

### Fix

Divide by the coefficient of the substrate the BRENDA row matched on. The loop
already knows which one that is: `subs{k}`, and `substrCoeff` is built from the
same index, so `substrCoeff(k)` is its coefficient.

Checked with the geckopy port of this function on the `full_ecModel` tutorial:
26 of 4671 matched reactions change, all of them previously inflated, by factors
of 2, 3 and 4. No reaction changes which BRENDA row or match level it draws
from. The same fix with regression tests is in SysBioChalmers/geckopy#57.

The tutorial ecModel would need regenerating to pick this up.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbc4ca3311df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
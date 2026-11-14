# Issue

**Title:** Element on a list of identical integers indexed by a variable

## Description

Part of the work on the constraint Element, taken up again issue by issue (#280 stays open for reference). This PR deals with #281 only: when all the integers of a list are equal, `c[i]` is replaced by this integer, so that `c[i] == 2` is evaluated by Python (`satisfy()` receives `True`), and `minimize(c[i])` fails.

**Tests** (`test_constraints_global_element.py`, new): each constraint is solved by ACE, CHOCO and cosoco, and compared with brute force; the expected solutions come from the semantics of element, whatever the fix:
- conditions with a variable (they work on master) and with an integer (`c[i] == 2`, `c[i] == 3`, `c[i] != 2`, `c[i] < 3`, `c[i] in {1, 2}`, `c[i] not in {1, 2}`: they fail),
- logical expressions (`(c[i] == 2) | (v == 1)`, `~(c[i] == 2)`, `If(v == 1, Then=c[i] == 3)`: they fail),
- the element used as an integer (`x[c[i]]`, `c[i] in x`, `v in [c[i], 4]`, `AllDifferent(c[i], v)`, `Count(x, value=c[i])`, `Sum()`): they work on master, and must keep working with the fix,
- matrices of identical integers (`m[j][k] == 2`, `m[j, k] == 3`: they fail) and of identical rows, a list of one integer (it fails),
- objectives: `minimize(c[i])` (it fails) and `minimize(c[i] + v)`; the expected result of `minimize(c[i])` is the optimum 2, or the message of #221 (`The objective is the constant 2: there is nothing to optimize`), according to the fix.

The indexes that can take a value outside the list (#282) are not tested here.

**Results on master** (821b50d): 51 passed, 39 xfailed (13 cases × 3 solvers, marked with #281).

The fix is not written yet: it will be chosen in this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `821b50dc68d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
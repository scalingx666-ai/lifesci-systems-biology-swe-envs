# Issue

**Title:** Constants of PyCSP3 (ConstraintDummyConstant) and element on a list of identical integers

## Description

(merged): the handling of the constants of PyCSP3 (`ConstraintDummyConstant`), and the fix of #281 (an element on a list of identical integers indexed by a variable), which relies on these constants.

**Fix of #281.** `c[i]`, with `c` a list of identical integers, was replaced by an integer of Python, so that `c[i] == 2` was evaluated by Python as a Boolean (refused by `satisfy()`) and `minimize(c[i])` failed. `c[i]` is now a `ConstraintDummyConstant`: `c[i] == 2` is always true (no constraint), `c[i] == 3` always false, `c[i] == v` gives `eq(v,2)` as before, and `minimize(c[i])` gives the message of #221. So that the uses of `c[i]` as an integer keep working (`x[c[i]]`, `-c[i]`, `c[i] in x`, `v in [c[i], 4]`, `AllDifferent(c[i], v)`, `Count(x, value=c[i])`, `m[j][c[i]]`), a constant is now accepted wherever an integer is.

**Commits**

| Commit | Change |
|---|---|
| c4f9c74 | An arithmetic operation between a constant and an integer (`c + 1`, `1 - c`, `c * 2`, `7 % c`...) gives a constant, and not an integer of Python (`c + 1 == 4` was evaluated by Python as a Boolean) |
| 668e318 | A decorator of the functions of global constraints (`AllDifferent` ... `Clause`) replaces the constants of their arguments (also in lists, tuples and generators) by their values; the inspector ignores the frames of the wrappers of decorators (`decorator_wrappers`), so that the comments of the model are kept |
| 57cd219 | The errors of arguments (missing or unknown parameter) are raised as Python does; `assert_fails()` of the harness ignores the frames of the decorator |
| bd1a1f2 | The constants among the values of a membership are replaced by their values (`v in [c, 4]`, `Sum(x) in [c, 4]`; not for the memberships of tuples, i.e. tables); `c in x` (`ListVar`) and `c in t` (`ListInt`) |
| 19f719d | : a variable in a list written literally (a tuple for Python), as `v in [x[0], x[1]]`, gives a member constraint, as for a list; a list (or a tuple) of variables and integers, as `v in [x[0], 2]`, is handled as the set of its values |
| 7482bc7 | : `c[i]` on identical integers gives a constant; the marks of #281 removed; the constraints always false are marked for ACE and CHOCO (table with an empty set of supports) |
| 65b9085 | Tests only: `v != 4` posted in the tests of memberships, so that a model whose membership is always true is solved |
| 67a888e | A constant as an index of a matrix (`m[j][c]`, `m[c, j]`, `m[j, c]`, `m[c, c]`) is replaced by its value: `m[j][c]` gave an element on all the variables of the matrix (wrong, found in TrainScheduling, whose lengths are identical in one instance) |

**Tests** (`test_constants.py`, `test_constraints_global_element.py`): constants with integers, unary operators, as indexes (of lists and of matrices), in global constraints (with the comments of the model), in memberships; elements on identical integers; member of a list written literally. Each fix comes with tests failing without it.

**Results** at 67a888e: whole suite: 12290 passed, 938 skipped, 945 xfailed, 0 failed. PyCSP3-models (one instance per model): the 415 XCSP3 files are identical to the ones of master (fbe0611), with the same compilation time (247.6 s, 250.6 s).

**Not done:** a constant in a set (`v in {c[i], 4}`) is refused by Python (`unhashable type`), as an element already is (`v in {d[i], 4}`); the order of the operands of `c + v` and `c * v` is not kept (`add(v,3)`), not changed so as not to change the XCSP3 of models.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbe0611a579e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
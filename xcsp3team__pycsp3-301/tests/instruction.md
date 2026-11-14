# Issue

**Title:** Element with an index outside the list

## Description

Part of the work on the constraint Element, taken up again issue by issue (#280 stays open for reference). This PR deals with #282: an index (variable or expression) that can take a value outside the indexes of the list was not detected for a list of identical integers (since #300, `c[i]` is a constant, so that the index is lost in every use of `c[i]`), for a matrix of identical rows (only the first row was kept), and for an expression as index of a matrix (`m[j][k + 1]`, `m[j, k + 1]`, `m[j + 1, k]`, restricted without error).

**Decisions** (taken in this PR):
- an index that can be outside the list is no longer an error: it is accepted with a warning (not displayed with `-force_element_index`);
- an element posted directly (or in a conjunction posted directly, as a term of a constraint posted directly, or in an objective) restricts its index to the list, with the same form as `-force_element_index` before (`index == aux` and the element on `aux`);
- in a logical expression (`|`, `~`, `If`, `imply`, `iff`, `xor`), an element whose index is outside the list does not hold, as in MiniZinc: the smallest subexpression containing it becomes `(index in the indexes) & ...`, `aux` being equal to the index (or to its smallest value) by a table, so that `aux` is a function of the index, also below a negation. This is the core of #284 (its tests in #280 are to be checked next).

**Commits**

| Commit | Content |
|---|---|
| 1b7911d | Unit tests of an element with an index outside the list () |
| 3211ab2 | Unit tests of an element on identical integers with an index outside the list () |
| 749a2d9 | The fix (): guards created when the element is built, nothing posted then; `satisfy()` and the objectives post `index == aux` at the level of the model, and add the condition and the table in a logical expression; the negation is handled when it is built (PyCSP3 pushes it down, `eq` becoming `ne`); identical integers give a constant only defined when the index is in the list, without auxiliary variable for the index |
| 67af2b2 | A comparison of Boolean expressions with a 0/1 variable or a 0/1 integer, as the reification `b == conjunction(x[i] == 2, ...)`, is a logical expression too (); found while checking ArithmeticTarget |
| ba7965d | The variables of an argument written as a string (matrix of allDifferent, lex and element, tuples of noOverlap in two dimensions, literals of clause) are kept apart (`variables`), so that the guards of their elements are found (): they were lost for an allDifferent matrix that cannot be compacted (always the case with an element in it) and for clause, the index being then not linked to its element at all (`index == aux` not posted, unlike master with `-force_element_index`); found in review |
| eda075b | A tuple, a set, a frozenset or a generator given in a list of `satisfy()` is handled as a list (): `handle_guards()` only went through lists, so that the guard of an element in a set or a frozenset was lost (index not linked to the element), and the one of an element in a logical expression of a tuple was posted as `index == aux` (index restricted for the whole model); a generator built its elements after `handle_guards()`, whose guards were lost; `satisfy()` now changes into lists the generators of a list before `handle_guards()`; found in review |
| 604b7fe | An index that can never be an index of the list gives a warning (`element_index_never`, not displayed with `-force_element_index`) instead of an error, as in MiniZinc (): the error was raised when the element was built, before its context was known, and only for a variable (the domain of its auxiliary variable was empty), so that an element in a logical expression was refused; the auxiliary variable (and the condition of a list of identical integers) now gets all the indexes of the list: posted directly, the model is unsatisfiable; in a logical expression, the element never holds; found in review |
| 2b215dd | The indexes of a guard are stored as computed (): `sorted()` only changed a range into a list, the values being already sorted by `possible_range()` or given by a range; no change of behavior; found in review |
| b37b9ff | The data of a guard (auxiliary variable, index, indexes, rank of creation) are gathered in a named tuple `Guard` (): `guard_rank` had the same keys as `guards`; `guarded` stays apart, its keys being all the variables depending on guards (not only the guards), completed later by `inherit_guards()` and `with_guards()`; no change of behavior; found in review |
| 6c4e32a | `index_guards()` is renamed `identical_index_guards()`, being only used for a list of identical integers or rows (); no change of behavior; found in review |
| f89316c | A 0/1 variable depending on guards gets the conditions of its guards under a negation, as an expression (): `~Table(scope=[x[i], y], ...)` with `i` outside `x` looped (`RecursionError`), the table being replaced by a 0/1 variable inheriting the guards; `self == 1` in `__invert__` did not build an expression (PyCSP3 simplifies `b == 1` into `b` for a 0/1 variable), so that `handle_guards()` posted the guards and returned the variable; now `not(and(in(i,set(0,1,2)),aux))`, 351 solutions with ACE as by brute force; found in review |

**Tests** (`test_constraints_global_element.py`): the cases expecting the error check the warning (and its absence with the option); the solutions are compared with brute force with and without the option (ACE, CHOCO, cosoco), each solution found once (so that `aux` is a function of the index); logical expressions on lists of variables, of integers and of identical integers (including `If(i < 3, Then=c[i] == v)`, as in LinearToProgram), on matrices, with an expression as index, and an objective. Reifications (`b == conjunction(...)`, `b != ...`): 24 tests that fail at 749a2d9. 8 new expected failures: CHOCO 4.10.15 (embedded) misses solutions of element on a matrix of variables with a variable as value (fixed in CHOCO 6.0.2, not reported); 1 mark of #294 (ACE on element on integers with an integer condition). Arguments written as strings (ba7965d): allDifferent-matrix, lex-matrix, clause and noOverlap in two dimensions, with an element in them (8 tests fail at 67af2b2); noOverlap with an element as origin or length is marked with #302 (an invalid XCSP3 file, also on master), cosoco is skipped on clause (s UNSUPPORTED) and marked with xcsp3team/cosoco#82 on a matrix given by explicit rows. Structures nested in a list of `satisfy()` (eda075b): a set, a frozenset, a tuple (not in first position) and a generator, with an element posted directly or in a disjunction (42 of the 48 tests fail at ba7965d). An index that can never be an index of the list (604b7fe): a variable, an expression and a list of identical integers, posted directly and in logical expressions, with the warning checked (38 of the 48 tests fail at eda075b; MiniZinc 2.8.5 gives the same results: model inconsistency, 54 and 81 solutions); the 4 new expected failures are ACE and CHOCO on the always false `c[i] == 2`, posted as a table with an empty set of supports.

**Results** at f89316c: element file 677 passed, 2 skipped, 40 xfailed; the files of the 13 models below are the same as at 6c4e32a; whole suite 12869 passed, 940 skipped, 975 xfailed, 0 failed; PyCSP3-models (415 instances): the same files as at eda075b (AccordionMini fails with a MemoryError on both sides, with a cap of 3 GB), and 402 of 415 the same as master (the 13 models below).

**Results** at 6c4e32a: element file 677 passed, 2 skipped, 40 xfailed; the files of the 13 models below are the same as at b37b9ff.

**Results** at b37b9ff: element file 677 passed, 2 skipped, 40 xfailed; the files of the 13 models below are the same as at 2b215dd.

**Results** at 2b215dd: element file 677 passed, 2 skipped, 40 xfailed; the files of the 13 models below are the same as at 604b7fe.

**Results** at 604b7fe: element file 677 passed, 2 skipped, 40 xfailed; the files of the 13 models below are the same as at eda075b.

**Results** at eda075b: element file 633 passed, 2 skipped, 36 xfailed; PyCSP3-models (415 instances): the same files as at ba7965d (eda075b changes `satisfy()` for every model).

**Results** at ba7965d: element file 585 passed, 2 skipped, 36 xfailed; allDifferent file 291 passed, 2 skipped, 7 xfailed; lex file 586 passed, 36 skipped, 23 xfailed; the files of the 13 models below are the same as at 67af2b2.

**Results** at 67af2b2: element file 573 passed, 20 xfailed (148 tests of logical expressions fail with the fix restricted to the level of the model); whole suite 12765 passed, 938 skipped, 955 xfailed, 0 failed.

**PyCSP3-models** (one instance per model): 402 of 415 identical to master (250.1 s vs 255.6 s). The others, solved with ACE (60 s) and, for the decisive cases, cosoco:

| Model | Master | This PR |
|---|---|---|
| LinearToProgram | optimum 6 | optimum 6 (the index, checked by `If`, was lost by the constant; restricting it gives UNSAT) |
| Gametes (MiniZinc 2023) | error; UNSAT with the option | optimum 3 (ACE, cosoco) |
| SteinerTree | error; UNSAT with the option | optimum 26003678 (ACE, cosoco) |
| ArithmeticTarget | error; UNSAT with the option | unknown in 60 s |
| SeatMoving | error; unknown with the option | SAT, bound 376 |
| Compression | 90 (SAT, not proved) | optimum 25 (ACE, cosoco) |
| Portal, Portal2 | optimum 9 | optimum 9 |
| RelToOntology | optimum 70802 (option) | optimum 70802 |
| SEDF | UNSAT (option) | UNSAT (elements as terms of a Cardinality posted directly); file 27 KB -> 7 KB |
| DC_MST, TD_TSP | SAT, same bounds in 60 s (option) | SAT, same bounds |
| RubiksCube | identical to master with the option | identical |

**Check with MiniZinc:** 11 of these models are translations of MiniZinc Challenge problems; the MiniZinc models were solved on the same instances (data compared) with MiniZinc 2.8.5 (OR-Tools CP-SAT, Chuffed, Gecode, 120 s each), and the XCSP3 files of master (with the option) and of this PR with ACE and cosoco (120 s each). With this PR, the optimum of MiniZinc is proved for 9 models and found (not proved) for DC_MST; ArithmeticTarget is UNSAT because its PyCSP3 model reads `numbers` from 0 whereas the indexes of the numbers are 1..n (xcsp3team/PyCSP3-models#4): with `numbers` indexed from 1, this PR accepts the optimal solution of MiniZinc (objective 5, also checked with CHOCO 6.0.2), and master rejects it. With master and the option, Gametes, SteinerTree and SeatMoving are UNSAT and Compression stays at 90 instead of 25. For these 13 models, the files of 67af2b2 are the same as those of 749a2d9.

Several files are smaller (ArithmeticTarget 158 KB -> 93 KB, Gametes 217 KB -> 82 KB): an index used in several elements of lists of the same length gives one auxiliary variable.

**Not done (later):** a constant of identical integers is an auxiliary variable with one value (`eq(aux,v)` instead of `eq(v,2)`); the documentation of `-force_element_index` and of the error on pycsp.org, now in xcsp3team/pycsp3-web#5 (to be merged once this PR is released). `Exist()` with at least three terms (compiled as `Count(...) >= 1`) and `Sum()` of Boolean terms, not handled term by term as a disjunction: left for another pull request for #284 (see the comment there).

**Found on the way (not fixed here):** `n_solutions()` reads the number of solutions of ACE written with a separator of thousands (`sols:1 344`, French locale) as 344; `satisfy_from_auxiliary()` posts the collected tables by `(index, aux) in table` in one generator, the second one giving `False` (not used by this PR, but probably reached with two reified tables); #302 (noOverlap with an element as origin or length).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a98bcfd7025a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
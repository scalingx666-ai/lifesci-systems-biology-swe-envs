# Issue

**Title:** Compare copies of the species mols when checking the thermo library for isomorphs

## Description

## Problem

`_thermo_lib_has_isomorph` in `arc/processor.py` compared the live species mols: `existing.mol.is_isomorphic(spc.mol)`. For two species with the same formula and multiplicity, as in any isomerization, the comparison reaches VF2, which sorts the vertices of both graphs. Atoms that were never labelled, as in a mol built from SMILES, keep that new order permanently.

The check runs in the thermo step, after each species' xyz and the reaction's `atom_map` were set. From then on a mol no longer follows its geometry: the `atom_order` written into the Arkane species YAML by `augment_arkane_yml_file_with_mol_repr`, and the BDE report's atom labels (`spc.mol.atoms[pivot-1]`), refer to the wrong atoms.

It was seen on a Ketoenol benchmark reaction (R1 ⇌ P1, both C2H4O): after the run, R1's mol no longer matched its xyz bonds and P1's had the wrong element at two positions, while `restart.yml`, written before the thermo step, was consistent.

## Change

Compare deep copies of the two mols, so the species keep their atom order. The comparison gives the same result as before; the same pattern is used in `arc/molecule/filtration.py` and `arc/molecule/resonance.py`. Both operands are copied because VF2 sorts both graphs. `save_order=True` was not used: after an earlier plain `is_isomorphic` call on the same graphs, VF2's module-level state skips the sort and the restore raises `ValueError: Number of vertices has changed`.

## Tests

`arc/processor_test.py`, 4 passed:
- `test_thermo_lib_has_isomorph_keeps_atom_order`: acetaldehyde vs vinyl alcohol keep their atoms in order. It fails with the original call and with either operand copied alone.
- `test_thermo_lib_has_isomorph_after_plain_isomorphism_check`: the check works after a plain `is_isomorphic` call on the same mols. It fails with `save_order=True`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3491f59963fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
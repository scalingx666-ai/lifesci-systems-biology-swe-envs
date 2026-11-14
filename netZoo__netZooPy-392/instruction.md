# Issue

**Title:** Fix COBRA install: add scikit-learn dependency + revamp install docs

## Description

.

### Problem
A user following the documented install (`git clone` → `cd netZooPy` → `pip3 install -e .`) could not run COBRA.

`netZooPy/cobra/cobra.py` imports `from sklearn.linear_model import LinearRegression, Lasso`, but `setup.py` did **not** list `scikit-learn` in `install_requires` (it was only in `requirements.txt`). Because `netZooPy/__init__.py` eagerly runs `from netZooPy import cobra`, a clean `pip install -e .` left **`import netZooPy` itself** broken with `ModuleNotFoundError: No module named 'sklearn'`, not just COBRA.

Separately, the reporter's `No module named 'netZooPy.cobra'` / `(unknown location)` errors come from an environment pitfall: running Python from the clone's parent directory (or a Jupyter/VS Code kernel that isn't the install env) makes the cloned `netZooPy` folder resolve as an empty namespace package that shadows the installed one.

### Changes
- **setup.py:** add `scikit-learn` to `install_requires` (the substantive fix).
- **README.md:** keep it minimal — only adds `from netZooPy.cobra import cobra` to the usage example.
- **docs/install/index.md:** revamp the install guide —
  - sync the dependency list with `setup.py` (was missing h5py, joblib, statsmodels, scikit-learn, click, tables, torch) and note pip installs them automatically; document CuPy as the optional GPU dependency;
  - recommend a virtual environment;
  - expand the Troubleshooting section to cover both failure modes above.

Troubleshooting content lives in the install guide (where users look) rather than the README.

### Verification
- Clean `python -m venv` + `pip install -e .` now auto-installs scikit-learn; `import netZooPy` and `from netZooPy.cobra import cobra` both succeed; `cobra()` runs in `nnls` and `MLE` modes.
- `tests/test_cobra.py` passes.
- Audited every submodule's module-load-time imports: `scikit-learn` was the only undeclared **hard** dependency. `cupy` is correctly optional (lazy, GPU-only); `patsy` is guaranteed via `statsmodels`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8008f18d30b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Fix headless stdout flooding

## Description

Running simulations through SynBioSuite can fail with `ERR_CHILD_PROCESS_STDIO_MAXBUFFER` when reb2sac progress output overflows Node.js's buffer in iBioSim-API. In headless mode, `Run.java` dumps every progress line (`Time=X`) to stdout, but nothing downstream uses them, they just accumulate until the buffer overflows.

- Skip `System.out.println` for lines successfully parsed as progress updates. Diagnostic output (warnings, errors) still prints.
- GUI path is unchanged, progress still goes through `parent.send()`.
- Add explicit transitive deps to `dataModels/pom.xml` so the module builds standalone.
- Fix http to https for osgeo Maven repo URL.
- Ignore `.sdkmanrc` in `.gitignore`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a170e0e1e083`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** CI: label our container, clean up only ours, and share a lock with the ReconXKG CI

## Description

Both CIs run on the same Blacknight runner and the same MATLAB image, and each started with docker rm -f of every MATLAB container, killing the other's running job. Cleanup now matches the label ci=cobra, and the MATLAB docker run takes flock on /var/lock/blacknight/matlab.lock (the ReconXKG CI takes the same lock) so the two run one at a time. Job timeout raised to 24 h because waiting for the lock counts toward it.

*Please include a short description of enhancement here*

**I hereby confirm that I have:**

- [X] Tested my code on my own machine
- [X] Followed the guidelines in the [Contributing Guide](https://opencobra.github.io/cobratoolbox/docs/contributing.html)
- [X] Selected `develop` as a target branch (top left drop-down menu)

*(Note: You may replace [ ] with [X] to check the box)*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `62812e7a480a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
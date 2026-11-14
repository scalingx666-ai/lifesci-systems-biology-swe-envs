# Issue

**Title:** Cancel superseded PR CI runs

## Description

> 🚧 **UNREVIEWED — awaiting review by @ChrisRackauckas.** Filed by an AI agent running as @ChrisRackauckas; Chris has not seen this.
> Harness: Claude Code 2.1.302 · Model: claude-sonnet-5-5
> Conversation: local subagent of the fleet-master session (no published session URL)

This PR should be ignored until reviewed by @ChrisRackauckas.

Adds a top-level `concurrency` group with `cancel-in-progress` to the `pull_request` workflows that lack one, so a new push to a PR cancels that PR's superseded run. `cancel-in-progress` is true only for `pull_request` events, so pushes to the default branch, tags and scheduled runs never cancel each other.

Workflows changed:
- `DependabotAutoMerge.yml`
- `DocPreviewCleanup.yml`
- `FormatCheck.yml`
- `RunicSuggestions.yml`
- `SpellCheck.yml`
- `benchmark.yml`

Workflows skipped:
- none

Verification: every edited file parses as YAML and differs from the original only by the `concurrency` key (checked programmatically). CI itself is the runtime check; I have not run the workflows locally.

## Risk assessment
- **Risk:** low (L3: CI configuration)
- **Blast radius:** PR CI runs only; no source, test or public API change. Pushes to the default branch, tags and schedules are unaffected by the conditional.
- **Evidence:** YAML round-trip check; an equivalent group with a `startsWith(github.ref, 'refs/pull/')` condition is already used by the existing CI workflows in these repos.
- **Independent review:** Codex gpt-6.1-sol rated it low (L3), high confidence: mechanical, PR-only CI configuration change with valid YAML and no group collision with the reusable workflows. It noted that a queued (not running) default-branch run can be replaced by a newer push to the same group, which `cancel-in-progress: false` does not prevent; that is the same behaviour as the existing `startsWith(github.ref, 'refs/pull/')` pattern.
- **Merge:** auto-merge candidate after an independent review

---
🤖 Posted by an AI agent — harness: Claude Code 2.1.302 · model: claude-sonnet-5-5
Conversation: local subagent of the fleet-master session (no published session URL)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `903f577bcbf5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Bump actions/github-script from 8 to 9

## Description

Bumps [actions/github-script](https://github.com/actions/github-script) from 8 to 9.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/github-script/releases">actions/github-script's releases</a>.</em></p>
<blockquote>
<h2>v9.0.0</h2>
<p><strong>New features:</strong></p>
<ul>
<li><strong><code>getOctokit</code> factory function</strong> — Available directly in the script context. Create additional authenticated Octokit clients with different tokens for multi-token workflows, GitHub App tokens, and cross-org access. See <a href="https://github.com/actions/github-script#creating-additional-clients-with-getoctokit">Creating additional clients with <code>getOctokit</code></a> for details and examples.</li>
<li><strong>Orchestration ID in user-agent</strong> — The <code>ACTIONS_ORCHESTRATION_ID</code> environment variable is automatically appended to the user-agent string for request tracing.</li>
</ul>
<p><strong>Breaking changes:</strong></p>
<ul>
<li><strong><code>require('@actions/github')</code> no longer works in scripts.</strong> The upgrade to <code>@actions/github</code> v9 (ESM-only) means <code>require('@actions/github')</code> will fail at runtime. If you previously used patterns like <code>const { getOctokit } = require('@actions/github')</code> to create secondary clients, use the new injected <code>getOctokit</code> function instead — it's available directly in the script context with no imports needed.</li>
<li><code>getOctokit</code> is now an injected function parameter. Scripts that declare <code>const getOctokit = ...</code> or <code>let getOctokit = ...</code> will get a <code>SyntaxError</code> because JavaScript does not allow <code>const</code>/<code>let</code> redeclaration of function parameters. Use the injected <code>getOctokit</code> directly, or use <code>var getOctokit = ...</code> if you need to redeclare it.</li>
<li>If your script accesses other <code>@actions/github</code> internals beyond the standard <code>github</code>/<code>octokit</code> client, you may need to update those references for v9 compatibility.</li>
</ul>
<h2>What's Changed</h2>
<ul>
<li>Add ACTIONS_ORCHESTRATION_ID to user-agent string by <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/github-script#695</a></li>
<li>ci: use deployment: false for integration test environments by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/github-script#712</a></li>
<li>feat!: add getOctokit to script context, upgrade <code>@​actions/github</code> v9, <code>@​octokit/core</code> v7, and related packages by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/github-script#700</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Copilot"><code>@​Copilot</code></a> made their first contribution in <a href="">actions/github-script#695</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/github-script/compare/v8.0.0...v9.0.0">https://github.com/actions/github-script/compare/v8.0.0...v9.0.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3a2844b</code></a> Merge pull request <a href="">#700</a> from actions/salmanmkc/expose-getoctokit + prepare re...</li>
<li><a href=""><code>ca10bbd</code></a> fix: use <code>@​octokit/core/</code>types import for v7 compatibility</li>
<li><a href=""><code>86e48e2</code></a> merge: incorporate main branch changes</li>
<li><a href=""><code>c108472</code></a> chore: rebuild dist for v9 upgrade and getOctokit factory</li>
<li><a href=""><code>afff112</code></a> Merge pull request <a href="">#712</a> from actions/salmanmkc/deployment-false + fix user-ag...</li>
<li><a href=""><code>ff8117e</code></a> ci: fix user-agent test to handle orchestration ID</li>
<li><a href=""><code>81c6b78</code></a> ci: use deployment: false to suppress deployment noise from integration tests</li>
<li><a href=""><code>3953caf</code></a> docs: update README examples from <a href="https://github.com/v8"><code>@​v8</code></a> to <a href="https://github.com/v9"><code>@​v9</code></a>, add getOctokit docs and v9 brea...</li>
<li><a href=""><code>c17d55b</code></a> ci: add getOctokit integration test job</li>
<li><a href=""><code>a047196</code></a> test: add getOctokit integration tests via callAsyncFunction</li>
<li>Additional commits viewable in <a href="https://github.com/actions/github-script/compare/v8...v9">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/github-script&package-manager=github_actions&previous-version=8&new-version=9)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a3a4220cc29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
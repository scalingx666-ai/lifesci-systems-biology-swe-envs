# Issue

**Title:** Bump astral-sh/setup-uv from 10.3.0 to 10.3.2 in the actions-deps group

## Description

Bumps the actions-deps group with 1 update: [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv).

Updates `astral-sh/setup-uv` from 10.3.0 to 10.3.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v10.3.2 🌈 update known checksums for 0.13.5</h2>
<h2>Changes</h2>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.13.5 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1103</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: update version references to v10.3.1 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1102</a>)</li>
</ul>
<h2>v10.3.1 🌈 preserve cache error class names in save-cache bundle</h2>
<h2>Changes</h2>
<p>This release includes a fix so that multiple concurrent workflows trying to upload the same cache no longer warn</p>
<p><code>##[warning]Failed to save: Unable to reserve cache with key ..., another job may be creating this cache.</code></p>
<h2>🐛 Bug fixes</h2>
<ul>
<li>fix: preserve cache error class names in save-cache bundle <a href="https://github.com/dannyward630"><code>@​dannyward630</code></a> (<a href="">#1093</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.13.4 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1099</a>)</li>
<li>chore: update known checksums for 0.13.2/0.13.3 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1098</a>)</li>
<li>chore: update known checksums for 0.13.1 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1094</a>)</li>
<li>Verify npm dependency signatures before builds <a href="https://github.com/zaniebot"><code>@​zaniebot</code></a> (<a href="">#1027</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: cache-dependency-glob matches relative to the working directory <a href="https://github.com/flange-ipb"><code>@​flange-ipb</code></a> (<a href="">#1092</a>)</li>
<li>docs: update version references to v10.3.0 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1090</a>)</li>
</ul>
<h2>⬆️ Dependency updates</h2>
<ul>
<li>chore(deps): roll up Dependabot updates <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1101</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>07a047e</code></a> chore: update known checksums for 0.13.5 (<a href="">#1103</a>)</li>
<li><a href=""><code>e1b8536</code></a> docs: update version references to v10.3.1 (<a href="">#1102</a>)</li>
<li><a href=""><code>18d369b</code></a> chore(deps): roll up Dependabot updates (<a href="">#1101</a>)</li>
<li><a href=""><code>4ad2329</code></a> chore: update known checksums for 0.13.4 (<a href="">#1099</a>)</li>
<li><a href=""><code>4bc6759</code></a> chore: update known checksums for 0.13.2/0.13.3 (<a href="">#1098</a>)</li>
<li><a href=""><code>c97f06e</code></a> fix: preserve cache error class names in save-cache bundle (<a href="">#1093</a>)</li>
<li><a href=""><code>8ca4be0</code></a> chore: update known checksums for 0.13.1 (<a href="">#1094</a>)</li>
<li><a href=""><code>b627d85</code></a> docs: cache-dependency-glob matches relative to the working directory (<a href="">#1092</a>)</li>
<li><a href=""><code>f8c8897</code></a> Verify npm dependency signatures before builds (<a href="">#1027</a>)</li>
<li><a href=""><code>f64d32b</code></a> docs: update version references to v10.3.0 (<a href="">#1090</a>)</li>
<li>See full diff in <a href="https://github.com/astral-sh/setup-uv/compare/1c37ad07a6a961277cf70c0d37d6f313000f5884...07a047e608db84b3d8c06cd9a7c7dcc9c355c18e">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=astral-sh/setup-uv&package-manager=github_actions&previous-version=10.3.0&new-version=10.3.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f89eee845841`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
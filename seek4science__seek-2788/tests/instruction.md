# Issue

**Title:** Bump rack from 3.2.7 to 3.2.8

## Description

Bumps [rack](https://github.com/rack/rack) from 3.2.7 to 3.2.8.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rack/rack/blob/main/CHANGELOG.md">rack's changelog</a>.</em></p>
<blockquote>
<h2>[3.2.8] - 2026-10-30</h2>
<h3>Security</h3>
<ul>
<li><a href="https://github.com/advisories/GHSA-5v64-555j-wjxm">GHSA-5v64-555j-wjxm</a> Multipart parser retains parsed data in its scan buffer, allowing denial of service via memory exhaustion.</li>
<li><a href="https://github.com/advisories/GHSA-wvg4-6p58-3gh3">GHSA-wvg4-6p58-3gh3</a> <code>Rack::Static</code> header rules were matched against an unnormalized path, allowing dot segments to bypass them.</li>
<li><a href="https://github.com/advisories/GHSA-2j8w-xcrc-x985">GHSA-2j8w-xcrc-x985</a> <code>Rack::Request#host_with_port</code>, <code>#base_url</code>, and <code>#url</code> returned the raw authority when it was invalid; <code>host_with_port</code> now returns <code>nil</code> in that case.</li>
<li><a href="https://github.com/advisories/GHSA-p8x9-v4hv-2w4g">GHSA-p8x9-v4hv-2w4g</a> Multipart requests with more than one <code>boundary</code> parameter were accepted when the first value was empty or began with a quote, semicolon, or comma, bypassing the guard added for CVE-2026-26961.</li>
</ul>
<h3>Fixed</h3>
<ul>
<li><code>Rack::Multipart::UploadedFile</code> now delegates keyword arguments to the wrapped tempfile. Calls such as <code>uploaded_file.readlines(chomp: true)</code> raised <code>TypeError</code> on Ruby 3.0+. (<a href="">#2481</a>, <a href="">#2501</a>, <a href="https://github.com/SeanLF"><code>@​SeanLF</code></a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5f511d7</code></a> Bump patch version.</li>
<li><a href=""><code>3e01d71</code></a> Update changelog.</li>
<li><a href=""><code>a295123</code></a> Reject multipart content types with a boundary parameter before the parsed one.</li>
<li><a href=""><code>49386f4</code></a> Don't leak invalid Host through host_with_port.</li>
<li><a href=""><code>18a07fe</code></a> Normalize static header rule paths before matching.</li>
<li><a href=""><code>244e75a</code></a> Remove parsed bytes from the multipart buffer while reading parts.</li>
<li><a href=""><code>3519905</code></a> Backport UploadedFile keyword forwarding fix (<a href="">#2501</a>)</li>
<li>See full diff in <a href="https://github.com/rack/rack/compare/v3.2.7...v3.2.8">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rack&package-manager=bundler&previous-version=3.2.7&new-version=3.2.8)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/seek4science/seek/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10632503d740`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
# Issue

**Title:** Bump msgpack from 1.8.2 to 1.8.7

## Description

Bumps [msgpack](https://github.com/msgpack/msgpack-ruby) from 1.8.2 to 1.8.7.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/msgpack/msgpack-ruby/blob/master/ChangeLog">msgpack's changelog</a>.</em></p>
<blockquote>
<p>2026-10-30 1.8.7</p>
<ul>
<li>Fix the Java version of the unpacker to never preallocate objects larger than
the buffered size (similar to the fix for the C unpacker in 1.8.1).</li>
</ul>
<p>2026-10-27 1.8.6</p>
<ul>
<li>Fix use-after-free when a recursive extension proc rescues, skips or resets.</li>
<li>Speed up decoding of oversized integers.</li>
<li>Avoid excessive memory allocation from crafted container headers.</li>
</ul>
<p>2026-09-11 1.8.5</p>
<ul>
<li>Prevent stack depth underflow when skipping from recursive unpacker.</li>
<li>Fix <code>Unpacker#skip_nil</code> to properly consume the buffer.</li>
<li>Fix some small difference in Factory registration of the Java implementation.</li>
<li>Fix some Factory/ext_type optimization edge cases.</li>
</ul>
<p>2026-07-28 1.8.4</p>
<ul>
<li>Fix <code>MessagePack::Buffer</code> to stop using already released memory page.
This could have caused data to leak across buffers when using the MessagePack::Buffer API
directly.</li>
</ul>
<p>2026-06-10 1.8.3</p>
<ul>
<li>Fix an integer overflow when parsing maps.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2c6a131</code></a> Release 1.8.7</li>
<li><a href=""><code>5a6edb3</code></a> Merge commit from fork</li>
<li><a href=""><code>ca0efc1</code></a> Prevent overallocation in the java unpacker</li>
<li><a href=""><code>2c34bb7</code></a> Release 1.8.6</li>
<li><a href=""><code>e89b5bc</code></a> Merge pull request <a href="">#410</a> from Watson1978/fix/buffer-append-string-uaf</li>
<li><a href=""><code>8731b86</code></a> Fix use-after-free when packing a string into an IO</li>
<li><a href=""><code>314d65d</code></a> Merge pull request <a href="">#408</a> from Watson1978/speedup/bigint-decode</li>
<li><a href=""><code>1a9f0e3</code></a> Merge pull request <a href="">#409</a> from Watson1978/fix/unpacker-container-prealloc</li>
<li><a href=""><code>c8d42d8</code></a> Fix excessive memory allocation from crafted container headers</li>
<li><a href=""><code>6bf285b</code></a> Speed up decoding of oversized integers</li>
<li>Additional commits viewable in <a href="https://github.com/msgpack/msgpack-ruby/compare/v1.8.2...v1.8.7">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=msgpack&package-manager=bundler&previous-version=1.8.2&new-version=1.8.7)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `766000e3a4b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
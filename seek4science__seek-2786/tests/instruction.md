# Issue

**Title:** Bump omniauth from 2.1.4 to 2.2.0

## Description

Bumps [omniauth](https://github.com/omniauth/omniauth) from 2.1.4 to 2.2.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/omniauth/omniauth/blob/master/CHANGELOG.md">omniauth's changelog</a>.</em></p>
<blockquote>
<h2>[2.2.0] - 2026-10-22</h2>
<h3>Added</h3>
<ul>
<li>Add a <code>full_host</code> option for each strategy, as a string or a proc that takes the Rack env. It takes precedence over <code>OmniAuth.config.full_host</code>. (<a href="">#835</a>)</li>
<li>Ship RBS type signatures for OmniAuth in <code>sig/</code>.</li>
<li>Document the Rack env keys OmniAuth sets, CSRF protection, sending <code>origin</code> as a form field, and how <code>SameSite</code> session cookies affect the callback in the README. (<a href="">#909</a>, <a href="">#1075</a>, <a href="">#1048</a>, <a href="">#1149</a>)</li>
<li>Add this changelog.</li>
</ul>
<h3>Changed</h3>
<ul>
<li><code>omniauth.params</code> now includes params posted to the request phase's form, not just its query string, so they survive the POST-only request phase introduced in 2.0. The <code>authenticity_token</code> param is never included (see CVE-2017-18076 under 1.3.2). If your request form posts other fields, they now appear in <code>omniauth.params</code> and are stored in the session until the callback. (<a href="">#975</a>)</li>
<li><code>OmniAuth::Builder</code> builds its middleware stack on the first request and reuses it, instead of rebuilding every strategy on every request. Providers added after the first request are ignored. (<a href="">#1083</a>, <a href="">#970</a>)</li>
<li><code>Strategy#call</code> sends a request that isn't on the strategy's request or callback path straight to the app, instead of duplicating the strategy for it. It still duplicates it in test mode, with an <code>other_phase</code>, with path lambdas, or when the strategy overrides how <code>#call!</code> dispatches. Methods patched directly onto <code>OmniAuth::Strategy</code>, rather than overridden in a subclass, aren't detected, so a patched <code>#call!</code> no longer runs for requests outside the strategy's paths. (<a href="">#1172</a>)</li>
<li>Require Ruby 2.5 or later (was 2.2). (<a href="">#1167</a>)</li>
<li>Require Rack 2.2.8 or later (was 2.2.3), rack-protection 2.2.0 or later, and hashie 3.5.2 or later (was 3.4.6).</li>
<li>The gem now contains only <code>lib</code>, <code>sig</code>, the license, the README, the changelog, and the security policy.</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Run the <code>before_callback_phase</code> hook for mocked failures in test mode, as for real callbacks. (<a href="">#1043</a>, <a href="">#1171</a>)</li>
<li>Recognize callback paths with a format suffix, such as <code>/auth/:provider/callback.json</code>. (<a href="">#618</a>, <a href="">#1170</a>)</li>
<li>Don't fail callbacks when the app defines a method named <code>uid</code>, <code>info</code>, <code>credentials</code>, or <code>extra</code> on <code>Object</code>. (<a href="">#898</a>, <a href="">#1169</a>)</li>
<li>Don't add a calculated <code>name</code> to the info hash subsets returned by <code>slice</code>, <code>except</code>, <code>select</code>, and <code>reject</code>. (<a href="">#892</a>, <a href="">#1168</a>)</li>
<li>Collapse repeated slashes in the request path, as Rails routing does, so <code>//auth/:provider</code> from a misconfigured proxy reaches the strategy. (<a href="">#1079</a>)</li>
<li>Avoid &quot;instance variable not initialized&quot; warnings on Ruby before 3.0.</li>
</ul>
<h3>Security</h3>
<ul>
<li>Guard against forged hosts in callback URLs. Unless a <code>full_host</code> is set, OmniAuth builds the callback URL it sends to the provider from the request's <code>Host</code>, <code>X-Forwarded-Host</code>, or <code>Forwarded</code> header, which a client can forge. The new <code>OmniAuth.config.allowed_hosts</code>, a list of strings and regexps, makes the request and callback phases fail with <code>invalid_host</code> unless the request's host matches one of them. Until <code>full_host</code> or <code>allowed_hosts</code> is set, the request phase logs a warning. The README's <code>full_host</code> example, which copied the <code>Host</code> header, is fixed. (<a href="https://github.com/omniauth/omniauth/security/advisories/GHSA-m27g-v28p-f9fx">GHSA-m27g-v28p-f9fx</a>, CVE-2026-63183)</li>
<li>Run <code>request_validation_phase</code> before writing <code>omniauth.params</code> to the session, so a cross-site POST rejected by the authenticity check can no longer store attacker-controlled params. (<a href="">#1162</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0d38078</code></a> Release 2.2.0</li>
<li><a href=""><code>943b44f</code></a> Add allowed_hosts to guard against forged hosts</li>
<li><a href=""><code>a241c94</code></a> Make the shipped signatures loadable from other gems</li>
<li><a href=""><code>01142e0</code></a> Remove Tidelift from the README, funding, and security policy</li>
<li><a href=""><code>6a77c9b</code></a> Use the mutant 0.17.1 release</li>
<li><a href=""><code>3420866</code></a> Mark the dispatch check private and note patched methods</li>
<li><a href=""><code>1ee5e75</code></a> Skip duplicating the strategy for requests that aren't its own</li>
<li><a href=""><code>84a4774</code></a> Update the copyright year and list every gem owner as an author</li>
<li><a href=""><code>b74232c</code></a> Don't depend on the OS's wording of ECONNREFUSED in a spec</li>
<li><a href=""><code>8b4e509</code></a> Test on Windows and let unreleased Rubies fail</li>
<li>Additional commits viewable in <a href="https://github.com/omniauth/omniauth/compare/v2.1.4...v2.2.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=omniauth&package-manager=bundler&previous-version=2.1.4&new-version=2.2.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a52d43c17321`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
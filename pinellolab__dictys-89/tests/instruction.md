# Issue

**Title:** Bump docker/login-action from 3 to 4

## Description

Bumps [docker/login-action](https://github.com/docker/login-action) from 3 to 4.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.0.0</h2>
<ul>
<li>Node 24 as default runtime (requires <a href="https://github.com/actions/runner/releases/tag/v2.327.1">Actions Runner v2.327.1</a> or later) by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#929</a></li>
<li>Switch to ESM and update config/test wiring by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#927</a></li>
<li>Bump <code>@​actions/core</code> from 1.11.1 to 3.0.0 in <a href="">docker/login-action#919</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> from 3.890.0 to 3.1000.0 in <a href="">docker/login-action#909</a> <a href="">docker/login-action#920</a></li>
<li>Bump <code>@​aws-sdk/client-ecr-public</code> from 3.890.0 to 3.1000.0 in <a href="">docker/login-action#909</a> <a href="">docker/login-action#920</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.63.0 to 0.77.0 in <a href="">docker/login-action#910</a> <a href="">docker/login-action#928</a></li>
<li>Bump <code>@​isaacs/brace-expansion</code> from 5.0.0 to 5.0.1 in <a href="">docker/login-action#921</a></li>
<li>Bump js-yaml from 4.1.0 to 4.1.1 in <a href="">docker/login-action#901</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v3.7.0...v4.0.0">https://github.com/docker/login-action/compare/v3.7.0...v4.0.0</a></p>
<h2>v3.7.0</h2>
<ul>
<li>Add <code>scope</code> input to set scopes for the authentication token by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#912</a></li>
<li>Add support for AWS European Sovereign Cloud ECR by <a href="https://github.com/dphi"><code>@​dphi</code></a> in <a href="">docker/login-action#914</a></li>
<li>Ensure passwords are redacted with <code>registry-auth</code> input by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#911</a></li>
<li>build(deps): bump lodash from 4.17.21 to 4.17.23 in <a href="">docker/login-action#915</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v3.6.0...v3.7.0">https://github.com/docker/login-action/compare/v3.6.0...v3.7.0</a></p>
<h2>v3.6.0</h2>
<ul>
<li>Add <code>registry-auth</code> input for raw authentication to registries by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#887</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> to 3.890.0 in <a href="">docker/login-action#882</a> <a href="">docker/login-action#890</a></li>
<li>Bump <code>@​aws-sdk/client-ecr-public</code> to 3.890.0 in <a href="">docker/login-action#882</a> <a href="">docker/login-action#890</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.62.1 to 0.63.0 in <a href="">docker/login-action#883</a></li>
<li>Bump brace-expansion from 1.1.11 to 1.1.12 in <a href="">docker/login-action#880</a></li>
<li>Bump undici from 5.28.4 to 5.29.0 in <a href="">docker/login-action#879</a></li>
<li>Bump tmp from 0.2.3 to 0.2.4 in <a href="">docker/login-action#881</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v3.5.0...v3.6.0">https://github.com/docker/login-action/compare/v3.5.0...v3.6.0</a></p>
<h2>v3.5.0</h2>
<ul>
<li>Support dual-stack endpoints for AWS ECR by <a href="https://github.com/Spacefish"><code>@​Spacefish</code></a> <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#874</a> <a href="">docker/login-action#876</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> to 3.859.0 in <a href="">docker/login-action#860</a> <a href="">docker/login-action#878</a></li>
<li>Bump <code>@​aws-sdk/client-ecr-public</code> to 3.859.0 in <a href="">docker/login-action#860</a> <a href="">docker/login-action#878</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.57.0 to 0.62.1 in <a href="">docker/login-action#870</a></li>
<li>Bump form-data from 2.5.1 to 2.5.5 in <a href="">docker/login-action#875</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v3.4.0...v3.5.0">https://github.com/docker/login-action/compare/v3.4.0...v3.5.0</a></p>
<h2>v3.4.0</h2>
<ul>
<li>Bump <code>@​actions/core</code> from 1.10.1 to 1.11.1 in <a href="">docker/login-action#791</a></li>
<li>Bump <code>@​aws-sdk/client-ecr</code> to 3.766.0 in <a href="">docker/login-action#789</a> <a href="">docker/login-action#856</a></li>
<li>Bump <code>@​aws-sdk/client-ecr-public</code> to 3.758.0 in <a href="">docker/login-action#789</a> <a href="">docker/login-action#856</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.35.0 to 0.57.0 in <a href="">docker/login-action#801</a> <a href="">docker/login-action#806</a> <a href="">docker/login-action#858</a></li>
<li>Bump cross-spawn from 7.0.3 to 7.0.6 in <a href="">docker/login-action#814</a></li>
<li>Bump https-proxy-agent from 7.0.5 to 7.0.6 in <a href="">docker/login-action#823</a></li>
<li>Bump path-to-regexp from 6.2.2 to 6.3.0 in <a href="">docker/login-action#777</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v3.3.0...v3.4.0">https://github.com/docker/login-action/compare/v3.3.0...v3.4.0</a></p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4907a6d</code></a> Merge pull request <a href="">#930</a> from docker/dependabot/npm_and_yarn/aws-sdk-dependenc...</li>
<li><a href=""><code>1e233e6</code></a> chore: update generated content</li>
<li><a href=""><code>6c24ead</code></a> build(deps): bump the aws-sdk-dependencies group with 2 updates</li>
<li><a href=""><code>ee034d7</code></a> Merge pull request <a href="">#958</a> from docker/dependabot/npm_and_yarn/lodash-4.18.1</li>
<li><a href=""><code>1527209</code></a> Merge pull request <a href="">#937</a> from docker/dependabot/npm_and_yarn/proxy-agent-depen...</li>
<li><a href=""><code>d39362a</code></a> build(deps): bump lodash from 4.17.23 to 4.18.1</li>
<li><a href=""><code>a6f092b</code></a> chore: update generated content</li>
<li><a href=""><code>60953f0</code></a> build(deps): bump the proxy-agent-dependencies group with 2 updates</li>
<li><a href=""><code>62c6885</code></a> Merge pull request <a href="">#936</a> from docker/dependabot/npm_and_yarn/docker/actions-to...</li>
<li><a href=""><code>102c0e6</code></a> chore: update generated content</li>
<li>Additional commits viewable in <a href="https://github.com/docker/login-action/compare/v3...v4">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a3a4220cc29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
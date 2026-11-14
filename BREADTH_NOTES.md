# Build notes - Systems Biology & Network Modeling

Repo2RLEnv pr_diff (v0.9.6), Harbor-format output. Domain: systems-biology.

## Funnel

| Stage | Count |
|---|---|
| Domain candidates (deduped) | 203 |
| After active+star+noise filter | 78 |
| Final target list (cap 200) | 78 |
| Repos with >=1 task | 63 |
| Repos with 0 tasks | 15 |
| Total tasks (<=3/repo) | 132 |

## Generation

- Shared task bank: each repo generated once (pr_diff, limit=3,
  max_files_per_pr=15, min_loc_changed=2), 4-way concurrency,
  rate-limit-aware with .done checkpoint resume.
- Per-domain consolidation: rank by reward_calibration.loc_changed desc,
  keep at most 3 tasks per repo. Zero-yield repos are NOT fabricated.
- Overlap with the 3 published cancer editions is allowed (user decision);
  domains are independent selections, not a partition of one repo set.

## Zero-yield repos (informational, 15)

- oncologylab/craftgrn
- prathyvsh/formal-systems-in-biology
- saeyslab/multinichenetr
- genular/pandora
- pybel/pybel
- SysBioChalmers/yeast-GEM
- saezlab/CollecTRI
- iaconogi/bigSCale2
- dportik/Biotech-Job-Search-Engine
- PayamDiba/SERGIO
- jackbibby1/SCPA
- aertslab/SCope
- ZJUFanLab/scRank
- PEtab-dev/PEtab
- flatironinstitute/inferelator

## Caveats

- Static validation only; real grading needs an LLM judge key + Docker.
- inline_dockerfile mode skips image build (no Docker daemon needed to publish).
- Provider secrets in upstream diffs were redacted before public release.

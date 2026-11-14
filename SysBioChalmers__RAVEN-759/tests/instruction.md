# Issue

**Title:** fix: read RAVEN 3 model files, and tolerate a non-double rev

## Description

Lets RAVEN 2 read model files written by RAVEN 3 and raven-toolbox, so RAVEN 2 functionality stays usable against current models. Proposed for a 2.11.4 patch release.

Prompted by SysBioChalmers/Human-GEM#1143, where a user on RAVEN 2.11.3 could reach Human-GEM 2.1.0 through none of its formats.

## What RAVEN 2 could not read

All in `io/readYAMLmodel.m`, measured against the released Human-GEM 2.1.0 YAML:

| | effect |
|---|---|
| `- metaData: !!omap` | the exact-match case missed the tagged map, so the whole block was skipped — no `id`, `name`, `version` or `date`, **silently** |
| reaction-side `notes:` | only `rxnNotes` was a case in the reactions section, so the read **aborted**: `Unknown entry in yaml file: - notes: PXMP2 forms a non-selective pore...` |
| `ec-code` inside `annotation` | gathered as a MIRIAM instead of filling `eccodes`, which came back empty |
| `smiles` inside `annotation` | same, for `metSmiles` |
| `- genes: []` | inline empty list not recognised |
| `gecko_light` | only `geckoLight` was accepted |

The first two are what blocked Human-GEM 2.1.0 outright.

**Read tolerance only.** What this version writes is unchanged — it still emits `rxnNotes` and an untagged `metaData` — so RAVEN 2 output stays valid for older RAVEN, and this stays a patch-sized change.

## importModel: the model note

`importModel` looked for the note between `xhtml">` and `</body>`. RAVEN's own `exportModel` writes that, but a writer serialising a notes dictionary emits one `<p>key: value</p>` per entry and no `<body>` at all, carrying the note under its own key. The labelled entry is now taken when there is one — so the other entries (version, and whatever else the dictionary held) stay out of the note — falling back to the `<body>` text otherwise.

## mergeLinear: an integer rev

`mergeLinear` combines `rev` with a sparse logical:

```matlab
pos = sum(reducedModel.S(twoNonZero(i),involvedRxns).' > 0 | reducedModel.rev(involvedRxns));
```

MATLAB rejects that for an integer class — `Sparse integer array arithmetic operations are not supported` — and a model built outside RAVEN can easily carry an integer `rev` (cobrapy's `save_matlab_model` writes `np.array(reversibility) * 1`, which is `int64` on Linux/macOS). Coerced once on entry rather than failing several steps into ftINIT.

## metComps

Documented as an integer column rather than a double. A reader that turns the 1-based index into a position needs an integer, and MATLAB's own `save` narrows an integer-valued double to an integer type on disk in any case; both classes index `comps` identically.

## Verification

MATLAB R2024b on Vera, against the released Human-GEM files.

Human-GEM 2.1.0 YAML, previously a hard abort:

```
loaded: 32 fields, 12748 rxns, 8374 mets
  id "HumanGEM"   name "Generic genome-scale metabolic model of Homo sapiens"
  version "2.1.0"   date "2026-09-30"
  annotation 1   rev 1   eccodes 1   rxnNotes 1   subSystems 1   metComps 1
```

Model note through SBML:

```
annotation subfields: taxonomy, note
note: Genome-scale metabolic models are valuable tools to study metabolism...
```

`mergeLinear` on the released Human-GEM 2.1.0 `.mat`, whose `rev` is `int64`:

```
rev class before: int64
mergeLinear: OK (8751 rxns out)
```

The `.mat` itself is fixed separately in SysBioChalmers/raven-toolbox#168; this change means RAVEN 2 survives the files already published.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2156ff13ea86`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.
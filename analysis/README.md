# Reproducing the revised risk-judgment analyses

This script reproduces the quantitative analyses used in the revised manuscript
**Comparing Large Language Model and Human Cybersecurity Risk Judgments: A CIS
Controls-Based Study**. It uses archived data only: it makes no model/API calls
and performs no additional human data collection.

## Files and installation

Copy this `analysis` directory into the repository root, alongside:

- `results_final_scenarios.xlsx`
- `pesquisa-de-riscos-ciberneticos-respostas.csv`

Run from the repository root. Python 3.12 was used for verification; dependencies
are pinned in `requirements.txt`.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r analysis/requirements.txt
python analysis/analyze_r2.py
```

On Windows, activate with `.venv\Scripts\activate` instead. Input and output
locations can also be specified:

```bash
python analysis/analyze_r2.py --data-dir . --output-dir analysis/results
```

No local machine paths or temporary-package locations are embedded in the script.
Input files are read without modification. Outputs in the selected directory
are regenerated when the script is run.

## Input interpretation and validation

The human CSV is UTF-8 with an optional BOM and **semicolon-delimited**, with
quoted multiline headers. The script reads 50 records and 18 ratings per person.
The self-reported professional-level field defines:

- `All` / Group 0: all 50 participants;
- `Senior` / Group 1: 32 `Sênior` or `Especialista` participants;
- `Other` / Group 2: the remaining 18 participants.

The two subgroups are mutually exclusive and their union is Group 0. These are
professional-level groups, not groups inferred from years of experience.

From the workbook's `Comparações` sheet, the script reads the five **individual
conversation scores** for every item and model. Cached mean columns are not used.
It checks all 450 transcribed scores against the complete archived model responses.
`Deepseek` is retained as the workbook sheet identifier; it denotes DeepSeek.

Both elicitation instruments permitted scores from **0 to 10**. Every original
score, including 0 and fractional values, is retained. There is no rescaling,
zero-to-one conversion, or imputation. Human item means are recomputed from
individual responses, without intermediate rounding. Overall partner scores
are excluded from the 18-item comparisons.

## Bootstrap procedure

Defaults: **20,000 resamples**, seed **20261005**, NumPy **PCG64**.

1. Draw 32 human participants with replacement within Group 1 and 18 within
   Group 2. Retain all 18 ratings from each selected participant together.
2. Form the Group 0 bootstrap item means using the observed 32/50 and 18/50
   composition.
3. Independently draw five complete conversation profiles with replacement
   within each model. Retain all 18 scores together.
4. Recompute model and human item means and their mean signed difference, MAE
   and RMSE. For the human subgroup comparison, use only the human resamples.
5. Take the 2.5th and 97.5th percentiles (linear quantile interpolation).

Drawing order is Group 1, Group 2, then ChatGPT, Deepseek, Llama, Claude and Gemini.
This preserves the random-number sequence used for the original manuscript
calculations. All **18 items remain fixed**. Resampling does not create new
observations or increase the original sample size.

Intervals are exploratory and conditional on the selected items, observed
profiles and recorded protocol. They assume exchangeability within resampled
groups. Convenience recruitment and only five conversations per model limit
their interpretation and nominal coverage. They do not establish population
representativeness or uncertainty for new items, organizations or model versions.

## Quantities and outputs

- `metrics.csv`: 15 model–reference comparisons. Signed difference is model
  minus human. Includes MAE, RMSE, Pearson r, paired standardized difference
  `dz`, profile-bootstrap intervals, and secondary paired tests with `df=17`.
  `p_holm_15` adjusts the family of **15** tests.
- `item_summary.csv`: 54 group–item rows, with unrounded human means, human
  sample SDs, and model means. Suitable as the source for tables and plots.
- `average_profile_comparisons.csv`: correlations calculated **after** averaging
  model means within items, not averages of the model-specific correlations.
- `transcription_audit.csv`: all 450 text-versus-transcription checks.
- `results.json`: all results, the human subgroup comparison, variability,
  individual disagreement, source SHA-256 hashes and software versions.

MAE and RMSE are discrepancies relative to human judgments, not errors against
objectively established cybersecurity risk. `dz` standardizes across the 18
item differences; it is not an individual-level effect size.

For traceability, the output also retains Spearman correlation, item-based t
intervals (`t_ci_bias`), a human subgroup Welch test, and conversation-variability
summaries from the original analysis script. These additional outputs should
not be confused with the **primary profile-bootstrap intervals** described in
the manuscript. Item-based t intervals and profile-bootstrap intervals reflect
different sources of variation. The Welch test is not part of the 15-test Holm
family, which concerns model–reference paired tests only.

`results.json` also reports descriptive individual disagreement: absolute score
differences for the same item across distinct unordered human pairs or all
participant–conversation pairs, then averaged over pairs and the 18 items.
These are not MAE between aggregate profiles. Overlapping pairs are not treated
as independent cases for significance tests.

The `reference_results` directory contains outputs generated with the default
settings and verified against the calculations used during manuscript revision.
Source hashes identify the exact data-file versions used. Results may change if
the inputs, seed, resample count, library versions, or drawing order change.

## Publication scope

This package replaces the earlier exploratory analysis that included a linear
score transformation. That transformation is **not** included here. This script
and its reference results have been prepared for repository upload; their
presence here does not mean that they have already been published online.

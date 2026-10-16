# Verification performed on 12 October 2026

The public script was executed with 20,000 resamples and seed 20261005 using the archived data files.

- All 450 text-versus-transcribed model scores matched.
- All 15 original-scale comparisons matched the archived revision analysis, including the three bootstrap intervals per comparison (225 numeric fields checked; relative/absolute tolerance 1e-12).
- The human subgroup metrics and bootstrap interval matched.
- Human/conversation variability and descriptive individual disagreement matched.
- Holm-adjusted p-values matched the 15-comparison revision export.
- Input SHA-256 hashes matched the archived revision provenance; input files were not modified.
- No linear score transformation or model/API execution is included.

Versions and exact data hashes are recorded in reference_results/results.json. Execution of the code was verified; this is not a claim of statistical validity or generalizability beyond the limitations described in README.md and the manuscript.

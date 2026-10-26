# Research Results CSVs

This folder contains CSV tables extracted from the supplied Final Project Archive and one
cross-phase model comparison derived by joining the supplied Phase I and Phase II model
tables by the `model` field.

## Files
- `attack_vectors.csv`: Phase I attack-vector comparison.
- `phase1_per_model.csv`: supplied Phase I per-model metrics.
- `phase2_per_model.csv`: supplied Phase II per-model metrics.
- `secure_scores.csv`: supplied security-score ranking and stated formula.
- `summary_metrics.csv`: supplied overall summary metrics.
- `model_comparison_phase1_phase2.csv`: derived join of Phase I and Phase II model rows,
  with ranking and recommended role from `secure_scores.csv`.

## Data integrity notes
The original CSV values are preserved in the extracted source tables. The comparison file
joins the provided rows by model; it does not recompute the underlying experiment metrics.
Aggregate values and interpretations should be checked against the canonical trial-level
records and the paper's final methodology before public release. In particular, ensure that
metric definitions, denominators, exclusions, and the stated R0 interpretation are documented
and consistent across the paper and code.

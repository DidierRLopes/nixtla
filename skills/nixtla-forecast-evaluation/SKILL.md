---
name: nixtla-forecast-evaluation
description: Backtest and compare forecasts with Nixtla cross-validation and UtilsForecast metrics. Use for rolling-origin evaluation, model selection, leakage audits, per-series error analysis, and testing whether a forecasting change improves business outcomes.
---

# Nixtla Forecast Evaluation

Compare models on the information and forecast schedule that would exist in actual use.

## Workflow

1. Define the forecast origin, horizon, refresh cadence, refit policy, series eligibility, primary metric, and business weighting. Reserve a final test period before model selection.
2. Build chronological rolling or expanding windows. Use the same cutoffs, future keys, feature availability, and scoring population for every candidate and the simple baseline.
3. Fit preprocessing, feature selection, calibration, augmentation, and model adaptation using only eligible history within each fold. Verify that saved models also respect the cutoff.
4. Run each library's `cross_validation` with explicit `h`, `n_windows` or test size, `step_size`, and `refit`. Library defaults differ; inspect the installed signature.
5. Evaluate predictions by `(unique_id, cutoff, ds)` where windows overlap. Specify model columns so features and metadata are not scored as predictions. Supply training-only history to scaled metrics with the correct cutoff-specific scale.
6. Report per-series, horizon, segment, and aggregate performance, including baseline-relative improvement and regressions. Include runtime and interval quality when those matter. Select on tuning folds and score the final choice once on the untouched period.

## Rules

- Never random-split time-series observations or evaluate fitted history as a future forecast.
- Inner joins can hide missing forecasts. Check the expected scoring keys before computing metrics.
- MAPE is unsuitable around zero targets; MASE/RMSSE need a nonzero training seasonal-error denominator. Report undefined cases rather than silently dropping them.
- Overlapping windows are dependent observations. Do not present their row count as an independent sample size.
- Read [recipes](references/recipes.md) for metric and cutoff handling; use [sources](references/sources.md) for library-specific cross-validation behavior and multi-objective selection.

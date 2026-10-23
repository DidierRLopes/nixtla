---
name: nixtla-probabilistic-forecast
description: Quantify forecast uncertainty with Nixtla prediction intervals, quantiles, and ConformalForecast calibration. Use for coverage diagnostics, calibrated ranges, quantile objectives, adaptive uncertainty, or transferring intervals to new series or regimes.
---

# Nixtla Probabilistic Forecasting

Produce uncertainty estimates whose units, calibration history, and coverage interpretation are explicit.

## Workflow

1. Establish whether the decision needs marginal intervals, quantiles, or joint path risk, and choose the target coverage or quantile loss. Use simulation when the decision depends on cumulative demand or simultaneous events.
2. Check the selected forecaster's native uncertainty capability. Use its supported probabilistic loss or interval API, or calibrate point forecasts using training-only residual windows. Read [recipes](references/recipes.md) before selecting a conformal adapter or method.
3. Separate model training, calibration, and later evaluation. Verify effective calibration samples per series and horizon; short or ragged panels can have fewer samples than the requested number of windows.
4. Choose split conformal for a stationary baseline, CQR for a quantile-capable model, weighted methods for justified shift handling, or adaptive methods for sequential feedback. Verify capabilities before calibration and preserve array axes.
5. Evaluate coverage, width, and a proper probabilistic score by horizon and segment on later observations. For online methods, predict first and update only when the corresponding truth arrives.
6. Deliver interval or quantile tables, calibration dates and assumptions, diagnostics, and any series without sufficient data. State whether coverage is marginal, per-series, or simultaneous.

## Rules

- A 95% interval is a coverage target, not a guarantee for every future observation or arbitrary distribution shift.
- TimeGPT uses percent-valued `level` and fractional `quantiles`; do not pass both. Conformal `alpha=0.1` corresponds to 90% target coverage.
- Repeatedly recalibrating on the evaluation period invalidates a fixed holdout claim. A sequential test must score each prediction before consuming its truth.
- Do not sum marginal interval endpoints to estimate an aggregate quantile. Use joint samples with validated dependence.
- The [source catalog](references/sources.md) covers native uncertainty, ConformalForecast methods, adapters, diagnostics, and transfer.

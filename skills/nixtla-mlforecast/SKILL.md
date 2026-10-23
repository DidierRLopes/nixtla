---
name: nixtla-mlforecast
description: Train feature-based time-series models with Nixtla MLForecast and scikit-learn, LightGBM, or XGBoost. Use for lag and rolling features, global panel models, direct versus recursive forecasting, target transforms, or incremental forecast updates.
---

# Nixtla Machine Learning Forecasting

Build a leakage-safe tabular forecasting pipeline with explicit feature availability and evaluation.

## Workflow

1. Establish the panel, frequency, horizon, seasonal patterns, static attributes, future-known drivers, and training budget. Include a seasonal-naive comparison.
2. Select lags and shifted rolling transformations that have enough history per series. Use MLForecast lag transforms rather than computing unshifted target aggregates on the complete dataset.
3. Instantiate a small estimator set and transformations appropriate to the target. Set `static_features` explicitly during fitting; dynamic columns require future values in `X_df`.
4. Choose recursive prediction for a compact initial model, or evaluate direct multi-horizon training when recursive error accumulation matters. Preserve sparse-horizon output semantics when using selected `horizons`.
5. Use chronological cross-validation with the intended refit schedule, feature availability, and horizon. Bound AutoML trials when using AutoMLForecast. Use training-only transformations and cutoff-specific future feature frames.
6. Fit the chosen pipeline on eligible history, predict the future grid, and return keyed forecasts, baseline metrics, feature configuration, and an update or retraining policy when requested.

## Rules

- MLForecast normally learns global regressors across series. An ID is not automatically a meaningful numerical feature.
- Default extra-column handling can treat dynamic features as static. Use `static_features=[]` when none are static.
- `update` appends observed history for lag state; it does not retrain the regressor. Evaluate update-only versus refit under drift.
- Do not manually reverse target transforms already inverted by MLForecast. Validate original-scale predictions.
- Read [recipes](references/recipes.md) for a minimal model, direct horizons, intervals, and persistence pointers; use [sources](references/sources.md) for advanced transforms, tuning, transfer, and distributed APIs.

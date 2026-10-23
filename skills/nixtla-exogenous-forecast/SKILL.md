---
name: nixtla-exogenous-forecast
description: Forecast with prices, promotions, holidays, weather, calendar features, or categorical attributes in Nixtla. Use when adding covariates, separating historical-only from future-known features, or fixing future exogenous alignment in TimeGPT, MLForecast, or NeuralForecast.
---

# Nixtla Forecasts with External Drivers

Use external drivers without letting unavailable future information enter the model.

## Workflow

1. Establish the forecast origin and classify every proposed feature as static, known in the future, or historical-only. Record when each value would actually be available, including reporting delays.
2. Keep only intended feature columns. Split before encoding, feature selection, imputation, or scaling. Separate realized future weather or prices from forecasts or planned values available at the origin.
3. Build the exact future `(unique_id, ds)` grid for each series. Join known-future features onto that grid, reject duplicates and missing required values, and exclude the future target.
4. Apply the selected library's feature contract from [recipes](references/recipes.md). TimeGPT uses `X_df` and historical/categorical lists; MLForecast needs explicit `static_features`; NeuralForecast uses model-level exogenous lists and `futr_df`.
5. Compare with and without covariates over identical chronological folds. Recreate each feature using its historical availability at each cutoff, including any separately forecast drivers.
6. Return the forecast, future feature table, availability assumptions, and measured change in the user's metric. Treat feature importance and scenario responses as predictive evidence, not causal effects.

## Rules

- A feature being present in a CSV does not make it known at prediction time. Historical-only variables must not be copied into future-known slots.
- Calendar and holiday effects must match local time and locale. Encode categorical features consistently across history and future data.
- Do not use a positional merge, blanket forward fill, or future target to manufacture a complete feature grid.
- Use the [source catalog](references/sources.md) for holiday helpers, categorical support, and the selected model's exogenous capabilities. Do not assume all StatsForecast or NeuralForecast models accept all feature types.

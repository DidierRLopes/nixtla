---
name: nixtla-statsforecast
description: Build fast local statistical forecasts with Nixtla StatsForecast. Use for ARIMA, ETS, Theta, MSTL, seasonal baselines, intermittent or sparse demand, and CPU forecasting across many independent series without a TimeGPT API key.
---

# Nixtla Statistical Forecasting

Choose a compact statistical baseline and model set matched to the data pattern and forecasting horizon.

## Workflow

1. Establish the frequency, horizon, seasonal periods, series count, and target constraints. Inspect available history, sparse demand, multiple seasonalities, and exogenous requirements.
2. Validate a long-format panel. Keep calendar frequency separate from season length: daily observations and weekly seasonality mean `freq="D"`, `season_length=7`.
3. Include `Naive` or `SeasonalNaive` and a small relevant candidate set. Use AutoETS/AutoARIMA/AutoTheta for suitable series, MSTL for multiple seasonalities, or intermittent-demand models for sparse counts. See [recipes](references/recipes.md).
4. Use `StatsForecast.forecast` for memory-efficient fit-and-forecast when fitted objects are unnecessary; use `fit` then `predict` for reuse. Set `n_jobs` to the available CPU budget and avoid nested parallelism.
5. Compare models on rolling-origin windows matching the requested horizon and refit policy. Inspect failures and per-series regressions; report fallback use if a `fallback_model` is configured.
6. Deliver keyed future forecasts, baseline comparison, uncertainty if supported or calibrated, a plot, and the selected seasonality and model rationale.

## Rules

- Sparse demand is not missing data. Keep real zeros and avoid MAPE as the primary metric for zero-heavy targets.
- Do not assume every model supports native intervals or exogenous regressors. Use conformal calibration where supported and enough training history exists.
- Fit exogenous preprocessing inside each fold and supply complete future driver values through the supported `X_df` argument.
- Benchmark complex candidates against the same simple baseline; automatic model selection does not establish superiority.
- Use [sources](references/sources.md) for individual model contracts, exogenous support, and distributed variants.

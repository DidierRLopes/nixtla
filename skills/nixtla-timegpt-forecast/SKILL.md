---
name: nixtla-timegpt-forecast
description: Generate single-series or multi-series forecasts with Nixtla TimeGPT. Use for a fast zero-shot forecast of demand, sales, energy, traffic, or other time-series targets through the hosted API or a chosen TimeGPT deployment.
---

# Nixtla TimeGPT Forecasting

Produce a usable TimeGPT forecast and evidence that it matches the requested future grid.

## Workflow

1. Identify the target, series keys, forecast origin, frequency, horizon, and desired uncertainty. Preserve the user's choice of hosted API, Azure, R, or another existing deployment.
2. Inspect the installed `nixtla` version and the matching SDK signature. Configure `NixtlaClient` through `NIXTLA_API_KEY` or the deployment's existing secret configuration. If credentials are unavailable, produce runnable code and state that the API call was not executed.
3. Validate a long-format panel: unique ID/time pairs, regular per-series timestamps, finite numeric targets, and adequate history. Pass `freq` explicitly when known, particularly with Polars or custom calendars.
4. Start with a zero-shot forecast. Supply only intended feature columns; use the external-driver recipe when covariates are requested. Check available models with `list_models()` when supported rather than assuming a model name is enabled.
5. Verify one row per requested future ID/time pair, no unexpected duplicates or missing predictions, and ordered interval bounds if requested. Join to actuals by keys for a chronological holdout or rolling-origin comparison against a seasonal-naive baseline.
6. Deliver the runnable code or notebook, forecast table, plot with the forecast boundary, and a short explanation of horizon, frequency, model, and any unexecuted calls.

## Rules

- `h` counts observations, not calendar duration. Monthly, daily, hourly, and business-calendar horizons differ.
- Keep `level` and `quantiles` mutually exclusive. Inspect actual output columns instead of deriving them from the selected model name.
- Multiple IDs in a frame do not imply joint multivariate modeling. Enable `multivariate` only for a supported model and an explicit cross-series need.
- The source snapshot defaults to `timegpt-2.1`; older tutorials use `timegpt-1` variants. Use the installed SDK and account's available models to resolve differences.
- Do not claim accuracy gains or production readiness from an in-sample plot. Read [recipes](references/recipes.md) for the minimal call and deployment choices; consult [sources](references/sources.md) for the selected interface.

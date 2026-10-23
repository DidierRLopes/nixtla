---
name: nixtla-neuralforecast
description: Train deep learning time-series models with Nixtla NeuralForecast. Use for NHITS, NBEATS, TFT, PatchTST, transformer or multivariate models, neural hyperparameter tuning, transfer learning, and model checkpoint workflows.
---

# Nixtla Neural Forecasting

Train a neural forecasting model against a meaningful baseline with explicit horizon, context, scaling, and validation.

## Workflow

1. Establish the horizon, frequency, number and lengths of series, seasonal behavior, feature availability, compute budget, and whether a truly multivariate model is required.
2. Validate the panel, keep static features in one row per ID, and declare model-level future, historical, and static exogenous lists. Check model capabilities before selecting a large architecture.
3. Start with a compact model such as NHITS or an architecture justified by the task. Set `h`, `input_size`, loss, scaler, seed, and bounded `max_steps`. Check that every usable series supplies context plus training and validation windows.
4. Fit with a chronological validation region for early stopping or tuning. Use Auto models only with explicit trial and resource limits. Keep the final test period out of architecture and hyperparameter selection.
5. Compare with simple statistical or machine-learning baselines using identical origins, feature information, and metrics. Set cross-validation `refit` deliberately; NeuralForecast defaults can differ from other Nixtla libraries.
6. Forecast with a complete `futr_df` when needed, verify the requested future keys, and save the model plus schema, dependencies, training cutoff, and configuration. Confirm load-and-predict behavior if persistence is requested.

## Rules

- A global neural model over many IDs is not necessarily a multivariate architecture. Models requiring `n_series` or aligned channels need their own data contract.
- Distinguish model window scaling from `NeuralForecast(local_scaler_type=...)`; do not stack scalers without a reason.
- Use `hist_exog_list` for variables unavailable in the future. Never feed held-out target values through `futr_df`.
- Forecast loss, validation loss, and the final business metric may differ. Evaluate in the original target units.
- Read [recipes](references/recipes.md) for training and persistence; use [sources](references/sources.md) for the selected architecture's constraints and specialized objectives.

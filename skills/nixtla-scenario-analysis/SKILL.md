---
name: nixtla-scenario-analysis
description: Explore what-if forecasts, joint simulation risk, and forecast explanations with Nixtla TimeGPT. Use for price or promotion scenarios, cumulative demand and capacity risk, correlated series, SHAP contributions, or historical predictive signal analysis.
---

# Nixtla Scenarios and Forecast Explanations

Translate forecast scenarios into decision quantities while keeping predictive sensitivity distinct from causality.

## Workflow

1. Identify the decision quantity: future point demand, cumulative units, profit, capacity exceedance, a simultaneous event, or an explanation. Fix the baseline, horizon, scenario assumptions, and available drivers.
2. For deterministic what-if comparisons, hold history and model fixed and change only the intended future covariates. Label inputs as assumptions and inspect whether they lie within historically supported ranges.
3. For path-dependent decisions, use `simulate` and aggregate each `sample_id` across time before computing a quantile or event probability. For joint cross-series risk, request supported multivariate coupling and verify the returned `coupled` status.
4. For explanations, select forecast SHAP contributions, intervention sensitivity, or historical `explain` analysis according to the question. Read [recipes](references/recipes.md) before interpreting their different outputs.
5. Backtest the decision rule or scenario evaluation on historical origins when feasible. Use a bounded number of paths and check sensitivity to Monte Carlo sampling before reporting precise tail probabilities.
6. Deliver baseline/scenario outcomes, assumptions, uncertainty or explanation tables, and a clear statement of the predictive interpretation. Report unsupported coupling or unexecuted API calls.

## Rules

- Scenario changes, SHAP, intervention replacement, Granger-style analysis, and transfer entropy do not identify real-world causal effects.
- Marginal quantiles do not encode temporal or cross-series dependence. Do not calculate cumulative-demand risk by adding per-time quantiles.
- `multivariate=True` can fall back to `coupled=False`; do not silently treat independent samples as joint portfolio futures.
- Snapshot simulation cannot combine `num_partitions` with multivariate coupling. Check current SDK constraints before scaling.
- Use [sources](references/sources.md) for simulation limits, explanation schemas, retail planning, and advanced dependence methods.

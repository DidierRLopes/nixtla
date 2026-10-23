---
name: nixtla-hierarchical-forecast
description: Reconcile Nixtla forecasts so totals match across products, stores, regions, or time aggregations. Use for hierarchical or grouped forecasts, BottomUp and MinTrace reconciliation, coherent uncertainty, and nonnegative aggregate forecasts.
---

# Nixtla Hierarchical Forecasting

Produce forecasts that satisfy the actual aggregation structure and quantify accuracy at the levels users act on.

## Workflow

1. Identify bottom-level series, aggregation keys, overlapping groups, temporal levels, and target units. Establish whether the input contains raw bottom data or already aggregated totals so observations are not double-counted.
2. Build the hierarchy with the supported aggregation utility or use the supplied summing matrix and tags. Verify that historical totals agree with bottom-level sums and that every ID has one meaning.
3. Generate base forecasts on a shared future grid at the required levels. Keep IDs and ordering consistent with the summing matrix. Preserve in-sample predictions when covariance-based reconciliation requires residuals.
4. Compare BottomUp with a justified reconciliation method such as MinTrace. Use nonnegative reconciliation for nonnegative targets; independent clipping after reconciliation can destroy coherence.
5. Reconcile and verify that every parent equals the sum of its applicable bottom series at each horizon within numerical tolerance. Evaluate accuracy by hierarchy level and business weight, not just one aggregate score.
6. Deliver coherent forecasts, hierarchy definitions, coherence checks, and the base-versus-reconciled evaluation. For uncertainty, use a supported probabilistic reconciliation method rather than summing marginal endpoints.

## Rules

- Grouped structures can overlap. Summing all intermediate groups can double-count demand.
- MinTrace variants have different residual and covariance requirements. `ols` does not need an estimated residual covariance; shrinkage variants generally do.
- Temporal reconciliation requires compatible aggregation windows and complete periods. It is not just adding another categorical key.
- Read [recipes](references/recipes.md) for aggregation and reconciliation; use [sources](references/sources.md) for sparse matrices, temporal or cross-temporal layouts, and probabilistic methods.

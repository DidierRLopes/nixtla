---
name: nixtla-forecast-at-scale
description: Scale Nixtla forecasting or training across large panels and existing Spark, Dask, or Ray environments. Use for memory limits, partitioning, asynchronous TimeGPT jobs, distributed MLForecast, distributed neural training, and production batch forecasting.
---

# Nixtla Forecasting at Scale

Scale a verified forecasting workflow while preserving complete histories, bounded work, and output accounting.

## Workflow

1. Measure the current bottleneck on a representative workload: local memory, model fitting, feature generation, API latency, or output volume. Record the series count, history distribution, horizon, and required columns.
2. Start with the existing local or cluster interface. Use direct batched or parallel execution when sufficient; introduce a distributed backend only for a demonstrated need or an explicitly selected environment.
3. Choose the supported path from [recipes](references/recipes.md): StatsForecast over distributed frames, DistributedMLForecast with backend estimators, NeuralForecast distributed training, or TimeGPT dataframe partitioning and jobs. Do not treat these as interchangeable APIs.
4. Preserve each series' complete ordered history within the partition required by the chosen library. Co-partition and validate future features. Set worker and model thread budgets to avoid oversubscription.
5. Bound concurrency, request sizes, polling, and retry time. Keep submitted job identifiers; distinguish failed submission from unknown server acceptance so a retry does not duplicate expensive work.
6. Verify expected ID/time coverage, failures, duplicates, and finite outputs across all partitions. Compare a small distributed result with the local workflow, allowing for justified floating-point or stochastic differences. Deliver the execution code, resource settings, manifest, and measured bottleneck.

## Rules

- Do not collect a full distributed dataset to pandas just to inspect it. Sample for inspection and keep large output distributed until deliberately materialized.
- A TimeGPT job handle does not create additional account capacity; excessive client parallelism can increase throttling.
- Keep finite deadlines and terminal failure handling. A timed-out client is not proof the server never accepted a job.
- Do not repartition coupled simulation independently by series; the documented multivariate simulation rejects `num_partitions`.
- Use [sources](references/sources.md) for the selected backend's installation, persistence, serving, and partition contracts.

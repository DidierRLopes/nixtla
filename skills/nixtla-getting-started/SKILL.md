---
name: nixtla-getting-started
description: Get started with Nixtla and produce a verified first forecast. Use when new to Nixtla or the Nixtlaverse, setting up a first project, choosing between TimeGPT and local forecasting libraries, or unsure which Nixtla skill fits a use case. For an established workflow, use its specialist skill directly.
---

# Nixtla Getting Started

Take the user from their goal to a working first forecast, then identify the next
useful workflow. This skill works independently of the other Nixtla skills.

## Workflow

1. Establish what the user wants to predict or detect, their data source, timestamp frequency, forecast horizon, and any local-only requirement. Inspect an existing project before asking for information it already contains. Ask only for missing decisions that affect the first result.
2. Preserve a chosen library or deployment. Otherwise use the selection guide in [first forecast](references/first-forecast.md): TimeGPT for a requested hosted foundation-model workflow; StatsForecast for a simple local forecast without credentials; MLForecast for a feature-based regressor; NeuralForecast for an intentional neural-training workflow. For a beginner without a preference or credentials, start with the local example and explain the choice.
3. Reuse the project's Python environment and install only the selected path's dependencies. For TimeGPT, use `NIXTLA_API_KEY` through the existing secret configuration without displaying it. Check the installed SDK and supported model before using a documentation example.
4. Inspect the user's data and map series ID, time, and numeric target into long format. Check duplicates, per-series timestamp continuity, missing targets, and usable history. Explain any repair that changes observations. If no data was supplied, use the clearly labeled deterministic demonstration in the reference; do not present it as the user's demand.
5. Produce the first forecast and verify its future ID/time grid and finite predictions. If there is enough real history, reserve a chronological holdout and compare against a simple baseline. A successful demo proves setup; it does not prove accuracy on the user's problem. If the chosen hosted path lacks credentials, prepare runnable code and state which call remains unexecuted.
6. Deliver the code, forecast table or output file, exact rerun command, and the selected backend, frequency, and horizon. Recommend a specialist workflow only when it advances the user's stated goal. The first forecast or an explicit prerequisite-blocked handoff is the completion condition; a library recommendation alone is insufficient.

## Next workflow

- Data repairs: `nixtla-time-series-data`. Forecast quality: `nixtla-forecast-evaluation`.
- Hosted zero-shot forecasting: `nixtla-timegpt-forecast`; model adaptation: `nixtla-timegpt-finetune`.
- Local models: `nixtla-statsforecast`, `nixtla-mlforecast`, or `nixtla-neuralforecast`, according to the chosen method.
- Prices, promotions, or weather: `nixtla-exogenous-forecast`. Outlier monitoring: `nixtla-anomaly-detection`.
- Prediction ranges: `nixtla-probabilistic-forecast`. Totals that must add up: `nixtla-hierarchical-forecast`.
- What-if decisions or joint risk: `nixtla-scenario-analysis`. Large workloads: `nixtla-forecast-at-scale`.
- Controlled test data or training augmentation: `nixtla-synthetic-data`.

If a specialist skill is installed, read it when that workflow becomes relevant.
If it is not installed, explain which skill would help and continue the supported
first-forecast path here. Do not assume sibling folders survived a single-skill
installation or install the whole collection as a prerequisite.

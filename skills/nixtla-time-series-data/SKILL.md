---
name: nixtla-time-series-data
description: Prepare and repair time-series data for Nixtla forecasting. Use for wide-to-long conversion, duplicate timestamps, missing dates or targets, irregular calendars, resampling, and multi-series input validation.
---

# Nixtla Time Series Data Preparation

Turn source data into a forecasting-ready panel while preserving the meaning of each observation.

## Workflow

1. Establish the series key, timestamp, target, forecast origin, frequency, horizon, and aggregation semantics. Distinguish transactional events from already aggregated measurements.
2. Inspect types, duplicate `(id, time)` keys, ordering, timezone and daylight-saving behavior, per-series lengths, gaps, missing targets, and valid zeros or negatives. Report the affected series and rows before changing them.
3. Convert to long format with `unique_id`, `ds`, `y`, or pass supported custom column names. Resolve duplicate keys using domain meaning; do not silently keep the last row.
4. Reindex each series on its intended calendar. Use `fill_gaps(..., start="per_serie", end="per_serie")` unless a shared panel origin is required. A regular business calendar is different from lost observations.
5. Split at the forecast origin before fitting imputers, scalers, encoders, or augmentation. Refit these inside each backtest fold. Impute separately within each series and preserve an audit of inserted or changed rows.
6. Verify unique keys, regular per-series timestamps, numeric targets, usable history, and a complete future feature grid. Return the cleaned panel, issue report, column mapping, and a small before/after sample.

## Rules

- Never equate missing observations, no recorded sales, and true zero demand without evidence. Stockouts may censor demand.
- Preserve real negative values and leading zeros unless their removal is justified by the use case. Do not run case-specific automatic cleaning as a default.
- TimeGPT documentation conflicts on target `NaN` support. Require finite targets for a portable workflow; preserve gaps as explicit `NaN` during diagnosis and verify backend support before leaving them unresolved.
- Interpolation across a backtest cutoff leaks information. Within an online stream, use only observations available at the prediction time.
- Read [recipes](references/recipes.md) for gap handling, audits, and calendar decisions. Use the [source catalog](references/sources.md) for the applicable backend's data contract.

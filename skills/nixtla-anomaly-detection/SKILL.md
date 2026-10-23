---
name: nixtla-anomaly-detection
description: Detect unusual time-series observations with Nixtla. Use for historical outlier discovery, recent-window monitoring, local or global anomaly thresholds, and tuning false alerts in operational metrics, sensors, demand, or traffic.
---

# Nixtla Anomaly Detection

Distinguish retrospective investigation from monitoring and produce an interpretable anomaly table.

## Workflow

1. Identify the monitoring objective, series, cadence, detection latency, and cost of missed events versus false alerts. Determine whether the request is historical exploration or evaluation of an online decision.
2. Validate the panel and inspect missingness, calendar shifts, known events, and regime changes. Preserve the observed values; an unusual observation is not automatically corrupt data.
3. Use `detect_anomalies` for historical analysis or `detect_anomalies_online` for recent-window detection. Start with a small representative set. Configure `h`, `detection_size`, and `step_size` from the operational cadence, not copied tutorial values.
4. Choose local versus global thresholding deliberately. Use `threshold_method="univariate"` for per-series thresholds and `"multivariate"` for aggregate deviations across aligned related series. This parameter is separate from multivariate model forecasting.
5. Tune the threshold on historical replay. Compare precision/recall when incident labels exist; otherwise report alert rates, stability, and representative events without inventing ground truth. Measure the delay before an incident is flagged.
6. Deliver keyed scores/flags and available bounds, plots of representative flagged events, parameter choices, and a replay procedure. Explain how newly arriving observations become available to the next detection call.

## Rules

- Increasing `level` generally raises the detection threshold and reduces sensitivity. Validate actual alert behavior rather than promising a false-positive rate.
- Recent-window detection is an SDK computation, not an installed streaming service. Do not imply that invoking it creates an ongoing monitor.
- Retrospective fits can use information unavailable at an alert time. Do not report historical reconstruction as online performance.
- Keep alerts separate from automatic deletion or correction of observations.
- Read [recipes](references/recipes.md) for method selection and output handling; use [sources](references/sources.md) for threshold semantics and exogenous support.

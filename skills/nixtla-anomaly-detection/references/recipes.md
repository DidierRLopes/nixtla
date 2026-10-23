# Anomaly detection recipes

## Historical investigation

```python
from nixtla import NixtlaClient

client = NixtlaClient()
anomalies = client.detect_anomalies(df=history, freq="D", level=99)
```

Inspect returned columns before interpreting scores. Plot the observed target,
expected value and available bounds, then highlight flags. Return the timestamps,
IDs, observed values, and the reason each point was flagged. A flag is a candidate
for investigation, not a diagnosis.

## Recent-window monitoring

```python
anomalies = client.detect_anomalies_online(
    df=history, freq="h", h=24, detection_size=168,
    step_size=24, level=99, threshold_method="univariate",
)
```

These daily blocks over hourly observations are an illustrative configuration.
Check that the series has enough preceding history for forecasting and threshold
estimation. The docs describe `detection_size` both as a recent analysis region and
as context used in threshold estimation; inspect the installed method and returned
date range when an exact latency or calibration boundary matters. `step_size`
controls successive windows, so overlaps can repeat alert evidence.

Global thresholding is useful for system-wide deviations. Align the series on the
same observation grid and evaluate the global alert unit. Do not count a global
flag copied onto several series as several independent incidents.

## Replay and alert burden

At each simulated decision time, provide only observations received by that time.
Save the origin, scored time, first alert time, and any overlap policy. Compare
thresholds at the same incident definition. Separate event-level precision and
recall from point-level metrics. Without labels, quantify alerts per day and
review false-alert candidates with the user.

When offline operation is required, the StatsForecast anomaly tutorial derives
anomalies from model residuals and intervals. Validate its residual calibration
chronologically; it is not an identical replacement for TimeGPT's anomaly API.
Exogenous anomaly models require the relevant historical drivers and the SDK's
supported anomaly-method signature, not an assumed forecast-style `X_df` call.

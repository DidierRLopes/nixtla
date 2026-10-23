# Uncertainty recipes

## Native library paths

- TimeGPT: `client.forecast(df=train, h=h, freq=freq, level=[80, 95])`, or `quantiles=[0.1, 0.5, 0.9]`, never both.
- StatsForecast: native supported model intervals or `ConformalIntervals(h=h, n_windows=...)` through `prediction_intervals`.
- MLForecast: fit with `mlforecast.utils.PredictionIntervals(h=h, n_windows=...)`, then request `level` at prediction time.
- NeuralForecast: a compatible `DistributionLoss`/quantile loss, or the documented `neuralforecast.utils.PredictionIntervals` calibration path.

Different libraries use different calibration classes and output naming. Import
the class from the selected library instead of interchanging similarly named types.

## ConformalForecast over StatsForecast

This is the API described by the supplied documentation; verify that the installed
release exposes these classes before using it. `train` is a single validated
series ending before an untouched evaluation period.

```python
from statsforecast import StatsForecast
from statsforecast.models import AutoETS
from conformalforecast import SplitConformal
from conformalforecast.adapters import StatsForecastAdapter

sf = StatsForecast(models=[AutoETS(season_length=7)], freq="D", n_jobs=1)
sf.fit(train)
adapter = StatsForecastAdapter(
    sf=sf, train_df=train, horizon=14, freq="D", model_name="AutoETS",
)
fitted = SplitConformal(alpha=0.1).calibrate_cv(adapter, n_windows=24)
history = train.sort_values("ds")["y"].to_numpy()[None, :]
prediction = fitted.predict(history)
# point: (n_series, 1, horizon)
# interval: (n_series, 1, horizon, 2), with lower/upper in the last axis
```

For a panel, use `conformalforecast.panel.long_to_panel` and preserve its series
index; do not reshape unsorted long data. The supplied implementation requires
at least `ceil(1 / alpha)` effective calibration windows per series. Check
`n_calibration_samples_` and handle `InsufficientCalibrationSamples` explicitly.
The default CV policy may use `refit=False`; some StatsForecast models such as
SeasonalNaive require `refit=True` for the adapter's forward-update path.

## Method and capability decisions

`calibrate`/`calibrate_cv` returns a fitted object; keep that result. CQR requires
quantile capability: MLForecastAdapter in this snapshot does not support it,
and NeuralForecastAdapter support depends on the fitted loss. CallableAdapter
supports supplied history-to-point functions but does not invent CV, refitting,
or quantiles. Check `supports(...)` or the documented capability errors.

WeightedSplit needs a justified target/source shift model. Raw pooling of errors
across unrelated scales is unsound; normalize scales or recalibrate on target
labels. AdaptiveConformalInference and related methods need ordered feedback;
do not update using future labels. Use SPCI, NEXCP, and aggregated adaptive methods
only when their specific assumptions and inputs match the use case.

These APIs are evolving. If unavailable in the installed distribution, use a
supported native calibration route or explain the dependency mismatch. Do not
silently substitute uncalibrated bands or install from an arbitrary branch.

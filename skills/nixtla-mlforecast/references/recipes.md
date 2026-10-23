# MLForecast recipes

Install `mlforecast`, `scikit-learn`, and `pandas` for this CPU example.
`train` contains only the validated ID/time/target columns, or declared features.

```python
from sklearn.linear_model import Ridge
from mlforecast import MLForecast
from mlforecast.lag_transforms import RollingMean
from mlforecast.target_transforms import Differences

mlf = MLForecast(
    models={"ridge": Ridge()}, freq="D", lags=[1, 7, 14],
    lag_transforms={1: [RollingMean(window_size=7)]},
    date_features=["dayofweek"], target_transforms=[Differences([7])],
)
mlf.fit(train, static_features=[])
forecast = mlf.predict(h=14)
```

The rolling mean at lag 1 excludes the current target. Differencing drops initial
history; combine lag and transformation requirements when checking short series.
For LightGBM or XGBoost, install the selected estimator separately and set its
thread budget together with MLForecast's `num_threads`.

## Direct versus recursive

`fit(..., max_horizon=h)` trains one model per step. It trades more fitted
estimators for less recursive target substitution. Newer releases also support
`horizons=[7, 14]`, which trains selected steps only and returns sparse output.
Check installed signatures before using selected horizons. Do not assert `h`
rows per series for a deliberately sparse forecast.

## Intervals and updates

```python
from mlforecast.utils import PredictionIntervals

mlf.fit(
    train, static_features=[],
    prediction_intervals=PredictionIntervals(n_windows=3, h=14),
)
forecast = mlf.predict(h=14, level=[80, 95])
```

Calibration consumes training windows; it is not an argument that can be added
only at prediction time. For newly observed rows, `mlf.update(new_observations)`
updates history and then `predict` uses the refreshed lag state. Compare that
policy with retraining, especially after structural changes.

## Transfer and persistence

`predict(new_df=...)` applies a fitted model to new histories where supported.
Tree regressors do not extrapolate smoothly to unseen target scales; evaluate
scale-invariant features or target normalization before claiming transfer works.
Use documented save/load or MLflow integration for the installed version and save
the feature schema, column mapping, frequency, cutoffs, and estimator dependencies.
Prediction callbacks and custom transforms require compatible executable code;
do not assume storing model weights alone recreates the pipeline.

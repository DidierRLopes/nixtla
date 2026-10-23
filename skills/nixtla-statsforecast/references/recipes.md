# Statistical forecasting recipes

Install `statsforecast` and the chosen DataFrame backend. `train` is a validated
long-format panel. This daily example assumes weekly seasonality.

```python
from statsforecast import StatsForecast
from statsforecast.models import AutoETS, SeasonalNaive

sf = StatsForecast(
    models=[SeasonalNaive(season_length=7), AutoETS(season_length=7)],
    freq="D", n_jobs=1,
)
forecast = sf.forecast(df=train, h=14, level=[80, 95])
```

Use a representative subset before scaling candidate count or parallel workers.
`forecast(..., fitted=True)` can retain fitted values for diagnostics; they are
not holdout predictions. When a later forecast must reuse fitted state, use
`sf.fit(train)` followed by `sf.predict(h=14)` instead.

## Model choice by data behavior

- A recurring single seasonal pattern: start with SeasonalNaive plus AutoETS or AutoARIMA. Pass a season length grounded in observations, not the number of forecasts requested.
- Several seasonal patterns: consider MSTL with the relevant seasonal lengths and inspect component stability. Do not treat one calendar label as a complete seasonal specification.
- Many zeros and intermittent demand: compare CrostonClassic, CrostonOptimized, CrostonSBA, ADIDA, IMAPA, or TSB as applicable. These differ in demand-size and arrival-rate assumptions; evaluate rather than selecting one by name.
- Changing probability of demand: assess TSB against an intermittent baseline. A flat point forecast can still be useful for inventory planning; validate aggregation over replenishment horizons.
- Volatility: ARCH/GARCH model a different objective from ordinary demand level forecasting. State whether the desired output is mean or conditional variance.

## Conformal intervals

```python
from statsforecast.models import ADIDA
from statsforecast.utils import ConformalIntervals

sparse = StatsForecast(models=[ADIDA()], freq="D", n_jobs=1)
forecast = sparse.forecast(
    df=train, h=14, level=[90],
    prediction_intervals=ConformalIntervals(h=14, n_windows=3),
)
```

Reserve enough history for calibration windows plus the model's own context.
Validate coverage on a separate later period. Some older sparse-demand tutorials
claim point forecasts only; the conformal tutorial documents interval wrappers.
Use supported calibration rather than inventing native distributions.

For repeated scoring, `sf.cross_validation(df=train, h=14, n_windows=3,
step_size=14, refit=True)` returns cutoffs and predictions. Retain the cutoff
when joining or evaluating overlapping windows.

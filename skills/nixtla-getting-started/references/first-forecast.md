# First forecast

## Choose the smallest useful path

| Situation | Starting path | Prerequisite |
| --- | --- | --- |
| Hosted foundation-model forecasts without training | TimeGPT through `nixtla` | API access and a supported model |
| First local forecast, seasonal baselines, statistical models | StatsForecast | Python and the input panel |
| Lag/calendar features with sklearn, LightGBM, or XGBoost | MLForecast | Chosen regressor and leakage-safe features |
| Train NHITS, TFT, or another deep architecture | NeuralForecast | Training history and a bounded compute budget |

Hierarchy, uncertainty, and evaluation are additional analytical jobs, not competing
point-forecast model families. Start with one model path. Do not install every
Nixtlaverse package or introduce a cluster just to learn the input format.

For a later promotion or price workflow, keep historical driver values alongside
the observed target, then prepare planned future values keyed by the same series
IDs and future timestamps. Those plans must be known at the forecast origin.
`nixtla-exogenous-forecast` covers the backend-specific feature contract.

## Local first run without an API key

Use the existing environment when available. In a new Python project, the local
example needs `pandas`, `numpy`, and `statsforecast`:

```bash
python -m pip install pandas numpy statsforecast
```

The complete example below uses demonstration data generated in memory, makes no
network requests, and writes `forecast.csv` in the working directory. Save it as
`first_forecast.py` and run `python first_forecast.py` in that environment.

```python
from pathlib import Path

import numpy as np
import pandas as pd
from statsforecast import StatsForecast
from statsforecast.models import AutoETS, SeasonalNaive

dates = pd.date_range("2025-01-01", periods=112, freq="D")
t = np.arange(len(dates))
history = pd.DataFrame({
    "unique_id": "demo",
    "ds": dates,
    "y": 50.0 + 0.1 * t + 8.0 * np.sin(2.0 * np.pi * t / 7.0),
})

forecaster = StatsForecast(
    models=[SeasonalNaive(season_length=7), AutoETS(season_length=7)],
    freq="D",
    n_jobs=1,
)
h = 14
forecast = forecaster.forecast(df=history, h=h)
expected_dates = pd.date_range(dates[-1] + pd.Timedelta(days=1), periods=h, freq="D")
assert not forecast.duplicated(["unique_id", "ds"]).any()
assert forecast["unique_id"].eq("demo").all()
assert forecast["ds"].sort_values().tolist() == expected_dates.tolist()
assert np.isfinite(forecast[["SeasonalNaive", "AutoETS"]].to_numpy()).all()
output = Path("forecast.csv")
forecast.to_csv(output, index=False)
print(forecast.to_string(index=False))
print(f"Saved {len(forecast)} forecast rows to {output.resolve()}")
```

`freq="D"` specifies daily timestamps. `season_length=7` specifies a weekly
pattern, and `h=14` requests fourteen future observations. Replace the
demonstration frame with eligible user history before making a business claim.
For multiple series, validate the future grid separately for each ID.

## Requested TimeGPT path

Install `nixtla` in the selected environment and configure `NIXTLA_API_KEY` using
the project's secret mechanism. Here `history` is a validated panel, using the
same three-column schema as the local example:

```python
from nixtla import NixtlaClient

client = NixtlaClient()
forecast = client.forecast(df=history, h=14, freq="D")
```

This transmits the supplied history to the configured service. Run it when the
user selected that service and credentials are configured. If credentials are
missing, do not silently change their chosen backend or fabricate a forecast.
Return the setup instructions and exact code that remains to be executed.

Check the installed package's model default and deployment support. The supplied
docs use newer model names than the `nixtla` 0.7.2 release verified for this
collection; methods such as `list_models`, `simulate`, or `jobs` may be absent.
The first forecast needs none of those newer methods.

## Authoritative sources

Open only the source relevant to the selected path or input issue:

- [TimeGPT quickstart](https://nixtla.io/docs/forecasting/timegpt_quickstart)
- [TimeGPT API key setup](https://nixtla.io/docs/setup/setting_up_your_api_key)
- [TimeGPT data requirements](https://nixtla.io/docs/data_requirements/data_requirements)
- [TimeGPT SDK reference](https://nixtla.io/docs/reference/sdk_reference)
- [Nixtlaverse overview](https://nixtlaverse.nixtla.io/index)
- [StatsForecast quickstart](https://nixtlaverse.nixtla.io/statsforecast/docs/getting-started/getting_started_short.html)
- [MLForecast quickstart](https://nixtlaverse.nixtla.io/mlforecast/docs/getting-started/quick_start_local.html)
- [NeuralForecast quickstart](https://nixtlaverse.nixtla.io/neuralforecast/docs/getting-started/quickstart.html)

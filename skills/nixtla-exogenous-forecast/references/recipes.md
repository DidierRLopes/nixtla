# External driver recipes

## TimeGPT

The following categorical call requires an SDK whose `forecast` signature includes
`categorical_exog_list`. That parameter is absent from `nixtla` 0.7.2. On a release
without it, use the documented consistent one-hot encoding of historical and
future categories, or keep only supported numeric features. Do not silently drop
the categorical driver or pass an unsupported keyword.

```python
forecast = client.forecast(
    df=history, X_df=future_features, h=14, freq="D",
    hist_exog_list=["observed_inventory"],
    categorical_exog_list=["promotion_type"],
)
```

Here `history` contains the target plus historical feature values.
`future_features` contains IDs, future timestamps, and future-known drivers such
as planned price and `promotion_type`, but no target or `observed_inventory`.
Check the installed SDK's handling of historical-only and categorical features.
Some older tutorials require manual one-hot encoding; current SDKs may accept
`categorical_exog_list` directly. Do not apply both encodings indiscriminately.
`date_features` can add calendar attributes; holiday functions should be applied to
both historical and future dates using the same locale.

## MLForecast

```python
mlf.fit(history, static_features=["store_type"])
forecast = mlf.predict(h=14, X_df=future_features)
```

Only list genuinely constant-per-series features as static. If all extra columns
are dynamic, pass `static_features=[]`; the default can classify extras as static.
`future_features` contains the dynamic drivers with complete future keys. Keep
lagged target and rolling target features in MLForecast's lag-transform machinery,
which applies the forecasting-time shift. Feature matrices built from unshifted
rolling targets leak the current target.

## NeuralForecast

```python
from neuralforecast import NeuralForecast
from neuralforecast.models import NHITS

model = NHITS(
    h=14, input_size=56, max_steps=100,
    futr_exog_list=["planned_price"],
    hist_exog_list=["observed_inventory"],
    stat_exog_list=["store_size"],
)
nf = NeuralForecast(models=[model], freq="D")
nf.fit(df=history, static_df=static_features)
forecast = nf.predict(futr_df=future_features)
```

`static_features` has one row per ID. Future exogenous variables also need their
historical values during training. Check the chosen model's supported feature
families. Forecast-time arrays and category mappings must use the training schema.

## Validate the future grid

Construct expected keys from the trained forecaster when a supported helper is
available, such as MLForecast's `make_future_dataframe`. Anti-join expected and
provided keys in both directions. Check per-series horizons and feature nulls.
For staggered series endings, do not use one global origin unless the workflow
explicitly aligns the histories first.

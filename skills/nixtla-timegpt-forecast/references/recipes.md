# TimeGPT forecast recipes

## Python zero-shot forecast

Install `nixtla`, `pandas`, and optionally `utilsforecast` for local evaluation.
`history` is a validated pandas or Polars frame with `unique_id`, `ds`, and `y`.

```python
from nixtla import NixtlaClient

client = NixtlaClient()  # Reads NIXTLA_API_KEY from the environment.
forecast = client.forecast(df=history, h=14, freq="D", level=[80, 95])
```

Use `id_col`, `time_col`, and `target_col` for custom names. A public sample dataset
in a tutorial is an example, not a replacement for the user's data.

The supplied documentation's default is TimeGPT-2.1, while the verified `nixtla`
0.7.2 release defaults to TimeGPT-1 and has no `list_models` method. Check the
installed signature and deployment's supported model configuration; use an explicit
known model when reproducibility matters. Do not invent an availability check on
an SDK that does not provide one.

Use `client.plot(history, forecast, level=[80, 95])` if the installed SDK supports it,
or plot keyed data with `utilsforecast.plotting.plot_series`. Mark the last observed
timestamp so fitted history is not mistaken for a future prediction.

## Product and deployment choice

- Hosted TimeGPT: use the existing API key. Keep secrets out of notebooks, output, and commits.
- Azure TimeGEN: retain the deployed endpoint and Azure configuration; read the Azure quickstart before changing initialization. Do not send Azure credentials to the hosted endpoint.
- Docker or private wheel: follow the corresponding deployment guide and verify that the licensed artifact and endpoint are already available. This collection does not supply them.
- R: use the documented R wrapper when the user is working in R rather than translating their project into Python.
- Excel: the add-in is a separate interface; do not assume a Python skill installs it.

Read the linked source for the requested deployment. Avoid hardcoded minimum history
or plan limits because they depend on the model, frequency, and account.

## Long horizons and use cases

Check accuracy across the actual horizon before choosing a long-horizon variant.
Compare with a seasonal-naive baseline on the same dates. For retail, distinguish
sales from uncensored demand; for energy, use the appropriate timezone and weather
availability; for traffic, retain business-calendar and event effects. Forecasted
asset prices are predictive distributions, not guaranteed returns.

For promoted products or weather-driven demand, use a future feature frame through
`X_df`. For recent outlier monitoring, use the anomaly methods instead of marking
ordinary forecast errors as confirmed anomalies. Fitted values returned by
`add_history=True` do not replace out-of-sample evaluation.

# Scenario and explanation recipes

## Simulate cumulative demand

This call requires a client exposing `simulate`; it is documented in the supplied
sources but absent from the verified `nixtla` 0.7.2 release. Check the installed
public API before generating executable simulation code. If it is unavailable,
offer supported deterministic scenario forecasts and explicitly leave joint risk
uncomputed. A point forecast or marginal interval is not a replacement for paths.

```python
paths = client.simulate(
    df=history, X_df=future_features, h=14, freq="D",
    n_paths=500, seed=42,
)
path_totals = paths.groupby(["unique_id", "sample_id"], observed=True)["TimeGPT"].sum()
quantiles = path_totals.groupby(level="unique_id").quantile([0.5, 0.9, 0.95])
```

`TimeGPT` is the documented simulated-value column; inspect output if the installed
version differs. Long-format rows also include future timestamps, `sample_id`, and
`coupled`. Check each ID/sample contains the complete horizon before aggregating.
Do not mix additional marginal-quantile output rows or columns into sample totals.
For a stockout probability, compare each sample's lead-time total with stock
available under the same replenishment policy. For capacity events, compute
whether any timestep exceeds capacity within each sample, then average flags.

For portfolio totals or simultaneous product demand, use `multivariate=True` and
require `coupled=True` for the relevant output. Series need a common origin and
adequate shared complete history. If coupling falls back, report that and avoid
a joint-risk conclusion. Do not simply align sample IDs from independent calls.

The snapshot caps paths and response size: `n_paths` is 1 to 10,000 and
`n_series * h * (n_paths + n_quantiles)` may not exceed 10,000,000. Verify current
limits and local memory before requesting a large result. Partitioning cannot
preserve multivariate coupling in the documented SDK.

## Compare scenarios

Create separate copies of the future feature table and change only the planned
driver. Provide each future-known driver in both history and `X_df`; do not also
declare it historical-only in `hist_exog_list`. Use keyword arguments for a
deterministic comparison: `client.forecast(df=history, X_df=scenario_features,
h=14, freq="D")`. Use the same supported seed for repeated scenario simulations to reduce
sampling noise, without claiming it identifies individual counterfactual worlds.
For coupled versus uncoupled diagnostics, the docs recommend different seeds and
comparison of cross-series statistics because the first seeded template may match.
Keep any clipping of negative simulated demand explicit; it changes the resulting
distribution and should be evaluated against a suitable constrained model.

## Explain the right object

Check method and parameter availability first. In the verified 0.7.2 release,
`forecast` accepts `feature_contributions`, but standalone `explain` and
`feature_contributions_type` are absent. Do not assume that supporting SHAP-style
forecast contributions also enables every explanation mode below.

- Forecast SHAP: `forecast(..., feature_contributions=True)` then copy `client.feature_contributions` before another call overwrites it.
- Sensitivity: add `feature_contributions_type="intervention"`. The model replaces numeric inputs by historical means and categorical inputs by modes; this is model response, not experimental treatment effect.
- Historical signals: `client.explain(df=history, features=[...], method="granger")`, or documented `transfer_entropy`, returns a ranking of lagged predictive information. Weights need not explain a particular forecast.

Use keyword arguments for `df`, `X_df`, and `h`; an older retail example contains
an ambiguous positional call. Declare categorical columns. Check historical-only
feature and `add_history=True` restrictions for the chosen explanation method.

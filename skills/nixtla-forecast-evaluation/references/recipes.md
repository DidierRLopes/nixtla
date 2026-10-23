# Evaluation recipes

## A rolling-origin table

`train` contains only data preceding the final holdout. This example uses
StatsForecast's CV; other Nixtla libraries expose related but distinct signatures.

```python
from statsforecast import StatsForecast
from statsforecast.models import SeasonalNaive, AutoETS
from utilsforecast.evaluation import evaluate
from utilsforecast.losses import mae, rmse

sf = StatsForecast(
    models=[SeasonalNaive(season_length=7), AutoETS(season_length=7)],
    freq="D", n_jobs=1,
)
cv = sf.cross_validation(
    df=train, h=14, n_windows=3, step_size=14, refit=True,
)
scores = evaluate(cv, metrics=[mae, rmse], models=["SeasonalNaive", "AutoETS"])
```

Preserve `cutoff` in both the results and scoring keys. The table already contains
observed targets in the supported CV APIs; do not merge actuals again on timestamp
alone and duplicate observations across windows.

## Metric decisions

- MAE: interpretable error in the target's units.
- RMSE: stronger penalty for large misses, still in target units.
- MASE or RMSSE: cross-series scaled errors, with seasonal training denominators. For each cutoff, compute the scale from that fold's eligible training data. Passing all history as `train_df` can leak later observations into earlier scales.
- MAPE and sMAPE: inspect denominator behavior around zero rather than treating percentages as universally comparable.
- Pinball/quantile loss and interval score: proper probabilistic scoring alongside observed coverage and width. A wide interval can achieve high coverage without being useful.

Do not conflate an equal-series mean with a volume-weighted score. In current
UtilsForecast docs, `weights="auto"` uses target sums in the evaluation window,
not training volume. If the business requires weights known at prediction time,
construct explicit training-period weights and document the population. Verify
`agg_fn="weighted_mean"` and weighting support in the installed version.

## Selection and operational comparability

TimeGPT `refit` interacts with adaptation; NeuralForecast often defaults to
`refit=False`, while statistical and ML APIs commonly default to refitting.
Make the intended policy explicit. Include model failures and missing series in
coverage accounting. Use fixed eligible series sets or clearly explain how each
model's supported population differs.

For accuracy/runtime or coverage/width tradeoffs, report a Pareto comparison
rather than hiding the chosen tradeoff in an arbitrary combined score. Dataset
loaders from DatasetsForecast can provide benchmarks; keep original splits and
frequency semantics, and do not mistake a benchmark win for domain validation.

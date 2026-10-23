# Synthetic data recipes

## Controlled seasonal fixture

Install `synforecast` and the requested frame backend.

```python
from synforecast.generators import SeasonalGenerator

panel = SeasonalGenerator(
    engine="polars", min_length=200, max_length=200, freq="D",
    seasonality_period=7, seasonality_amplitude=8.0,
    base_level=100.0, noise_level=2.0, seed=42,
).generate(n_series=4)
```

For a varied corpus, `synforecast.generate_series` draws from a broad pool;
`with_generator_col=True` can retain provenance where supported. `SynSet` composes
explicit generators into one panel. Record each generator and seed so benchmark
inputs can be recreated. Do not add generator identity to forecasting features
unless it would exist for the real task.

## Training augmentation

```python
from synforecast import SynAugment

augmented_train = SynAugment(seed=42).augment(train, n_augment=2)
```

`train` contains only the eligible real training observations. Inspect whether the
installed method includes originals and how it assigns synthetic IDs before
concatenating anything; do not duplicate originals. Fit separate forecasters on
observed-only and augmented training, then score the same untouched real future.
In verified SynForecast 0.2.0, augmentation includes originals and converts series
IDs to strings. Normalize ID types deliberately before joining results back to
the real panel; retain an explicit mapping if the source IDs are numeric.
Repeat seeds when claiming an accuracy effect. A generic pool may be useful for
pretraining, but matching frequency, target scale, and temporal structure matters.

## Inject known events

The documented generators support anomaly, changepoint, and missing-data options.
`ExogenousConfig(anomaly_flags=True)` can expose anomaly labels in versions that
provide it. Keep such labels out of forecasting features and use them only to
evaluate event detection. Preserve the clean reference before corruption when
measuring degradation against ground truth.

Choose missingness mechanisms consistent with the intended sensor or business
failure. Dropped timestamps and missing targets test different data contracts.
Multivariate missingness or common shocks require their documented dependence
controls; independent univariate generators do not create cross-series structure.

For robustness curves, keep the clean holdout and metric scale fixed across
corruption levels. In particular, computing MASE's denominator from progressively
more corrupted training data can make a worsening forecast appear better.
Specialized domain generators cover intermittent demand, energy load, clickstream,
IoT, and counts; read the selected source before assuming positivity or integer
support. Scale claims about real-world performance to the actual held-out evidence.

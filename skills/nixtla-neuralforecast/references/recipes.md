# NeuralForecast recipes

Install `neuralforecast` and use a compatible PyTorch environment.
`train` is a long-format frame containing eligible observations only.

```python
from neuralforecast import NeuralForecast
from neuralforecast.models import NHITS
from neuralforecast.losses.pytorch import MAE

model = NHITS(
    h=14, input_size=56, max_steps=100,
    scaler_type="robust", loss=MAE(), random_seed=42,
    enable_progress_bar=False, logger=False,
)
nf = NeuralForecast(models=[model], freq="D")
nf.fit(df=train, val_size=14)
forecast = nf.predict()
```

The context length and training steps are starter values, not tuned settings.
A small CPU smoke run can verify the workflow; it does not estimate the final
accuracy of a longer training run. With early stopping, configure the supported
validation interval and positive validation size. Inspect warnings about short
series or ignored model arguments instead of globally suppressing them.

## Choose architecture by information structure

NHITS is a useful starting point for long-horizon univariate outputs pooled over
a panel. NBEATS and interpretable variants may help with decompositions. TFT uses
rich covariates; PatchTST and other transformers have their own context and feature
constraints. Explicitly multivariate families such as TSMixer require aligned
channels and the configured series count. Check the specific model page rather
than treating all architectures as drop-in replacements.

For probabilistic outputs, select a compatible distributional or quantile loss,
or configure documented conformal calibration. Merely requesting levels does
not create a valid uncertainty model for every loss.

## Save and reload

```python
nf.save(path="./artifacts/nhits", save_dataset=False)
loaded = NeuralForecast.load(path="./artifacts/nhits")
reloaded_forecast = loaded.predict(df=train)
```

With `save_dataset=False`, pass eligible history again at prediction time. Avoid
unrequested overwrites. New documentation describes safer artifact formats and
explicit trust options for legacy pickle or remote artifacts. Do not set
`allow_pickle=True` or `trust_remote=True` as an automatic compatibility fix.
Use them only for artifacts whose provenance the user trusts, after checking the
installed load signature. Custom losses, optimizers, and callbacks may require
code to be supplied again.

`cross_validation` can evaluate several rolling origins. Set `refit` explicitly:
reusing a fitted network with updated context and retraining at each cutoff answer
different operational questions. See the source catalog for temporal classification,
robust objectives, distributed training, ONNX, and explainability when requested.

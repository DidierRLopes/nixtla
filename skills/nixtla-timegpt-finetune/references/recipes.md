# Fine-tuning recipes

## Inline adaptation

```python
adapted = client.forecast(
    df=train, h=14, freq="D", model=base_model,
    finetune_steps=10, finetune_depth=1, finetune_loss="mae",
)
```

`base_model` is a verified model available in the user's deployment. Ten steps is
an example, not a recommended optimum. Inline adaptation produces forecasts;
do not assume it returns a reusable model ID.

## Save and reuse

```python
model_id = client.finetune(
    df=train, freq="D", model=base_model,
    finetune_steps=10, finetune_depth=1, finetune_loss="mae",
)
forecast = client.forecast(
    df=train, h=14, freq="D", model=base_model,
    finetuned_model_id=model_id,
)
```

`finetune` returns an ID, not a DataFrame. `finetuned_models(as_df=True)` lists
artifacts, and `finetuned_model(model_id)` retrieves metadata in the documented
SDK. Use `finetuned_model_id` to continue adaptation from an existing artifact
only when intended. Do not set `output_model_id` to an existing production ID
without checking overwrite semantics.

The snapshot's SDK reference still types synchronous `finetune` with TimeGPT-1
variants while its async counterpart defaults to TimeGPT-2.1. Resolve support
using the installed signature and current deployment before issuing a request.
`list_models()` establishes model availability, not necessarily fine-tuning
capability. Do not use availability alone as proof that every operation is supported.

## Valid evaluation

Select configurations on rolling cutoffs within training history. Do not tune on
the final test period and then label the resulting score out-of-sample selection.
Keep the same feature availability, horizon, and metric for baseline and adapted
models. A saved model that already saw a scored period cannot be repaired simply
by passing shorter history to `forecast`.

For asynchronous execution, check `client.jobs.finetune` availability. Its job
result is the model ID. Keep the job handle and bounded polling settings so a
retry does not launch duplicate training jobs.

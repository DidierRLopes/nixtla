# Scaling recipes

## TimeGPT jobs and dataframe partitions

Use the blocking method for a simple bounded request or documented
`num_partitions` behavior. For explicit asynchronous control, current docs expose:

```python
job = client.jobs.forecast(df=history, h=14, freq="D", job_timeout_seconds=300)
result = job.wait(poll_timeout=360, cancel_on_timeout=True)
```

The verified `nixtla` 0.7.2 release does not expose `jobs`; use its blocking
`forecast` interface unless a compatible SDK is available. Do not add a thread or
queue service just to disguise a missing server-side job API.
Check installed support before using `jobs`. `job_timeout_seconds` bounds server
execution; `poll_timeout` bounds client polling. The SDK has adaptive polling, so
avoid adding another busy loop. Catch the documented JobError, JobTimeoutError,
and JobCancelledError separately from input errors. A timeout can request
cancellation but does not make completion impossible during the cancellation race.

Read timeouts and gateway failures during submission can leave acceptance unknown.
Do not blindly resubmit; retain diagnostics and use an existing handle if returned.
Async `jobs.*` calls do not accept `num_partitions` in this snapshot. The blocking
counterpart is the documented partitioned path; the job handle represents one job.
`jobs.detect_anomalies` mirrors the online detection contract, not the simpler
historical method.

## Select the actual distributed API

- StatsForecast accepts supported Spark, Dask, or Ray frames through its backend integration. Install the documented backend extras and verify a small forecast; avoid building a second orchestration layer around an already supported frame.
- MLForecast uses `mlforecast.distributed.DistributedMLForecast` and backend-specific model wrappers such as DaskLGBMForecast. A local sklearn estimator is not automatically a distributed estimator. Dask histories must remain within one partition per series; verify this after repartitioning.
- NeuralForecast distributed fitting uses `DistributedConfig`, an existing Spark workflow, shared partition storage, and compatible worker/GPU settings. It is different from locally tuning several independent models in parallel.
- NeuralForecast can train from supported partitioned Parquet inputs for large datasets. Follow ordering and batch contracts; do not assume passing arbitrary file paths preserves series boundaries.

Do not materialize the full output until its expected size fits memory. Forecast
rows scale with series times horizon; simulation additionally scales with paths.
Control nested estimator threads and worker counts together. Estimate memory for
features, fitted models, and outputs, not only raw input.

## Persistence and serving

Save preprocessing, schema, frequency, model dependencies and cutoff with the
artifact. Validate reload on a representative batch. Use existing MLflow or ONNX
integration only when deployment requires it. Model logging is not proof that
an online endpoint is running. Do not deploy services or create cloud resources
merely because a batch forecast was requested.

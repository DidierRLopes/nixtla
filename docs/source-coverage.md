# Documentation coverage

The complete source downloads were parsed into 449 page records on 2026-10-23:
90 from TimeGPT and 359 from Nixtlaverse. Each page boundary is identified by its
heading and `Source:` URL. The workflow catalogs below account for every record,
including explicit context-only treatment of company, legal, and contributor pages.
These assignments record topical coverage, not a claim that every documented model
or cloud deployment has been executed.

The collection distills operational decisions into skills and focused recipes.
Full source bodies are not vendored: they include duplicated tutorials, rendered
outputs, model catalogs, and changing service details. Each independently
installable skill carries its own relevant source links.

## Source snapshots

- [timegpt](https://www.nixtla.io/docs/llms-full.txt): 572,641 bytes; SHA-256 `ceabf7fe16ce807f1707d35ed917208f9147643c420b2a7c535f7a040e08b352`.
- [nixtlaverse](https://nixtlaverse.nixtla.io/llms-full.txt): 4,624,621 bytes; SHA-256 `58d452ed785d44e2de3fa77067a23be1da23cf1253c6a873df7d562517dbe069`.

## Handling documentation differences

- Missing target values: the TimeGPT quickstart rejects them, while the missing-values tutorial permits explicit NaNs on a complete timestamp grid. Recipes use finite targets for a portable default and require checking the selected backend before leaving NaNs.
- TimeGPT model names: newer pages use TimeGPT-2.1; older fine-tuning and long-horizon tutorials use TimeGPT-1 variants. The installed SDK and deployment capabilities determine valid calls.
- Sparse-demand uncertainty: older tutorials describe point forecasts only; newer conformal examples add calibrated intervals. The skills distinguish native distributions from calibration wrappers.
- Artifact loading and sparse hierarchy interfaces: documentation can describe APIs newer than the installed release. Recipes require checking signatures and avoid automatic trust flags or arbitrary source-branch installations.
- Published SDK capability: local verification installed `nixtla` 0.7.2, which defaults to TimeGPT-1 and lacks documented simulation, standalone explanation, async jobs, model listing, and categorical-list forecast arguments. The affected recipes make that boundary explicit. Source inclusion is not a claim of package availability.

## Workflow decisions

Separate skills follow different data contracts or validation obligations. External
drivers, evaluation, uncertainty, reconciliation, and simulation remain usable
across model families. Business examples such as retail demand, energy, and traffic
live within those workflows instead of creating overlapping domain copies.
Synthetic generation and conformal calibration have their own workflows because
their ground-truth and calibration rules differ from fitting a point forecaster.

## Page routing

| Source page | Workflow catalog |
| --- | --- |
| [Key Concepts](https://nixtla.io/docs/about/key-concepts) | `nixtla-timegpt-forecast` |
| [Privacy Notice](https://nixtla.io/docs/about/privacy-notice) | Context only: company/legal/contributor information |
| [Nixtla](https://nixtla.io/docs/about/sub-categoria) | Context only: company/legal/contributor information |
| [Terms and Conditions](https://nixtla.io/docs/about/terms-and-conditions) | Context only: company/legal/contributor information |
| [Add Exogenous Variables](https://nixtla.io/docs/anomaly_detection/exogenous_variables) | `nixtla-anomaly-detection`, `nixtla-exogenous-forecast` |
| [Quickstart](https://nixtla.io/docs/anomaly_detection/historical_anomaly_detection) | `nixtla-anomaly-detection` |
| [Controlling the Anomaly Detection Process](https://nixtla.io/docs/anomaly_detection/real-time/adjusting_detection) | `nixtla-anomaly-detection` |
| [Online (Real-Time) Anomaly Detection](https://nixtla.io/docs/anomaly_detection/real-time/introduction) | `nixtla-anomaly-detection` |
| [Local vs Global Anomaly Detection](https://nixtla.io/docs/anomaly_detection/real-time/univariate_multivariate) | `nixtla-anomaly-detection` |
| [Cancel an async job](https://nixtla.io/docs/api-reference/async-jobs/cancel-an-async-job) | `nixtla-forecast-at-scale` |
| [Get async anomaly_detection job status](https://nixtla.io/docs/api-reference/async-jobs/get-async-anomaly_detection-job-status) | `nixtla-anomaly-detection`, `nixtla-forecast-at-scale` |
| [Get async cross_validation job status](https://nixtla.io/docs/api-reference/async-jobs/get-async-cross_validation-job-status) | `nixtla-forecast-at-scale` |
| [Get async explain job status](https://nixtla.io/docs/api-reference/async-jobs/get-async-explain-job-status) | `nixtla-forecast-at-scale` |
| [Get async finetune job status](https://nixtla.io/docs/api-reference/async-jobs/get-async-finetune-job-status) | `nixtla-forecast-at-scale`, `nixtla-timegpt-finetune` |
| [Get async forecast job status](https://nixtla.io/docs/api-reference/async-jobs/get-async-forecast-job-status) | `nixtla-forecast-at-scale` |
| [Get async simulate job status](https://nixtla.io/docs/api-reference/async-jobs/get-async-simulate-job-status) | `nixtla-forecast-at-scale` |
| [Submit an async anomaly_detection job](https://nixtla.io/docs/api-reference/async-jobs/submit-an-async-anomaly_detection-job) | `nixtla-anomaly-detection`, `nixtla-forecast-at-scale` |
| [Submit an async cross_validation job](https://nixtla.io/docs/api-reference/async-jobs/submit-an-async-cross_validation-job) | `nixtla-forecast-at-scale` |
| [Submit an async explain job](https://nixtla.io/docs/api-reference/async-jobs/submit-an-async-explain-job) | `nixtla-forecast-at-scale` |
| [Submit an async finetune job](https://nixtla.io/docs/api-reference/async-jobs/submit-an-async-finetune-job) | `nixtla-forecast-at-scale`, `nixtla-timegpt-finetune` |
| [Submit an async forecast job](https://nixtla.io/docs/api-reference/async-jobs/submit-an-async-forecast-job) | `nixtla-forecast-at-scale` |
| [Submit an async simulate job](https://nixtla.io/docs/api-reference/async-jobs/submit-an-async-simulate-job) | `nixtla-forecast-at-scale` |
| [Compute model-agnostic feature importance weights](https://nixtla.io/docs/api-reference/compute-model-agnostic-feature-importance-weights) | `nixtla-scenario-analysis` |
| [Delete Fine-tuned Model](https://nixtla.io/docs/api-reference/delete-fine-tuned-model) | `nixtla-timegpt-finetune` |
| [Foundational Time Series Model Multi Series](https://nixtla.io/docs/api-reference/foundational-time-series-model-multi-series) | `nixtla-timegpt-forecast` |
| [Foundational Time Series Model Multi Series Anomaly Detector](https://nixtla.io/docs/api-reference/foundational-time-series-model-multi-series-anomaly-detector) | `nixtla-anomaly-detection` |
| [Foundational Time Series Model Multi Series Cross Validation](https://nixtla.io/docs/api-reference/foundational-time-series-model-multi-series-cross-validation) | `nixtla-timegpt-forecast` |
| [Foundational Time Series Model Multi Series Finetuning](https://nixtla.io/docs/api-reference/foundational-time-series-model-multi-series-finetuning) | `nixtla-timegpt-finetune` |
| [Foundational Time Series Model Online Multi Series Anomaly Detector](https://nixtla.io/docs/api-reference/foundational-time-series-model-online-multi-series-anomaly-detector) | `nixtla-anomaly-detection` |
| [Get single Fine-tuned Model](https://nixtla.io/docs/api-reference/get-single-fine-tuned-model) | `nixtla-timegpt-finetune` |
| [List Fine-tuned Models](https://nixtla.io/docs/api-reference/list-fine-tuned-models) | `nixtla-timegpt-finetune` |
| [List Models](https://nixtla.io/docs/api-reference/list-models) | `nixtla-timegpt-forecast` |
| [Validate Api Key](https://nixtla.io/docs/api-reference/validate-api-key) | `nixtla-timegpt-forecast` |
| [Audit and Clean Data](https://nixtla.io/docs/data_requirements/audit_clean) | `nixtla-time-series-data` |
| [Data Requirements](https://nixtla.io/docs/data_requirements/data_requirements) | `nixtla-time-series-data`, `nixtla-timegpt-forecast`, `nixtla-getting-started` |
| [Missing Values](https://nixtla.io/docs/data_requirements/missing_values) | `nixtla-time-series-data` |
| [Multiple Time Series](https://nixtla.io/docs/data_requirements/multiple_series) | `nixtla-time-series-data`, `nixtla-timegpt-forecast` |
| [Cross-validation Tutorial](https://nixtla.io/docs/forecasting/evaluation/cross_validation) | `nixtla-forecast-evaluation` |
| [Evaluation Metrics](https://nixtla.io/docs/forecasting/evaluation/evaluation_metrics) | `nixtla-forecast-evaluation` |
| [Evaluation Pipeline](https://nixtla.io/docs/forecasting/evaluation/evaluation_utilsforecast) | `nixtla-forecast-evaluation` |
| [Categorical Variables](https://nixtla.io/docs/forecasting/exogenous-variables/categorical_features) | `nixtla-exogenous-forecast` |
| [Find predictive signals in history](https://nixtla.io/docs/forecasting/exogenous-variables/causal-explanations) | `nixtla-exogenous-forecast`, `nixtla-scenario-analysis` |
| [Date/Time Features](https://nixtla.io/docs/forecasting/exogenous-variables/date_features) | `nixtla-exogenous-forecast` |
| [Holidays & Special Dates](https://nixtla.io/docs/forecasting/exogenous-variables/holiday_and_special_dates) | `nixtla-exogenous-forecast` |
| [Explain a forecast with SHAP](https://nixtla.io/docs/forecasting/exogenous-variables/interpretability_with_shap) | `nixtla-exogenous-forecast`, `nixtla-scenario-analysis` |
| [Numeric Variables](https://nixtla.io/docs/forecasting/exogenous-variables/numeric_features) | `nixtla-exogenous-forecast` |
| [Advanced explanations](https://nixtla.io/docs/forecasting/explanation/advanced-explanations) | `nixtla-scenario-analysis` |
| [Test forecast sensitivity](https://nixtla.io/docs/forecasting/explanation/intervention) | `nixtla-scenario-analysis` |
| [Understanding forecasts](https://nixtla.io/docs/forecasting/explanation/introduction) | `nixtla-scenario-analysis` |
| [Fine-tuning with a Specific Loss Function](https://nixtla.io/docs/forecasting/fine-tuning/custom_loss) | `nixtla-timegpt-finetune` |
| [Controlling the Level of Fine-Tuning](https://nixtla.io/docs/forecasting/fine-tuning/depth) | `nixtla-timegpt-finetune` |
| [Re-using fine-tuned models](https://nixtla.io/docs/forecasting/fine-tuning/save_reuse_delete_finetuned_models) | `nixtla-timegpt-finetune` |
| [Fine-tuning Tutorial TimeGPT](https://nixtla.io/docs/forecasting/fine-tuning/steps) | `nixtla-timegpt-finetune` |
| [Distributed Forecasting with Spark, Dask & Ray](https://nixtla.io/docs/forecasting/forecasting-at-scale/computing_at_scale) | `nixtla-forecast-at-scale` |
| [Time Series Forecasting with Dask](https://nixtla.io/docs/forecasting/forecasting-at-scale/dask) | `nixtla-forecast-at-scale` |
| [Time Series Forecasting with Ray](https://nixtla.io/docs/forecasting/forecasting-at-scale/ray) | `nixtla-forecast-at-scale` |
| [Time Series Forecasting with Spark](https://nixtla.io/docs/forecasting/forecasting-at-scale/spark) | `nixtla-forecast-at-scale` |
| [Improve Forecast Accuracy with TimeGPT](https://nixtla.io/docs/forecasting/improve_accuracy) | `nixtla-timegpt-forecast` |
| [Long-Horizon Forecasting with TimeGPT](https://nixtla.io/docs/forecasting/model-version/longhorizon_model) | `nixtla-timegpt-forecast` |
| [Uncertainty Quantification with TimeGPT](https://nixtla.io/docs/forecasting/probabilistic/introduction) | `nixtla-probabilistic-forecast` |
| [Prediction Intervals](https://nixtla.io/docs/forecasting/probabilistic/prediction_intervals) | `nixtla-probabilistic-forecast` |
| [Quantile Forecasts](https://nixtla.io/docs/forecasting/probabilistic/quantiles) | `nixtla-probabilistic-forecast` |
| [Simulation](https://nixtla.io/docs/forecasting/probabilistic/simulation) | `nixtla-probabilistic-forecast`, `nixtla-scenario-analysis` |
| [Scenario Analysis with Simulation](https://nixtla.io/docs/forecasting/probabilistic/simulation_scenarios) | `nixtla-probabilistic-forecast`, `nixtla-scenario-analysis` |
| [Bounded Forecasts](https://nixtla.io/docs/forecasting/special-topics/bounded_forecasts) | `nixtla-probabilistic-forecast`, `nixtla-timegpt-forecast` |
| [Hierarchical Forecasting](https://nixtla.io/docs/forecasting/special-topics/hierarchical_forecasting) | `nixtla-hierarchical-forecast` |
| [Irregular Timestamps](https://nixtla.io/docs/forecasting/special-topics/irregular_timestamps) | `nixtla-time-series-data` |
| [Temporal Hierarchical Forecasting with TimeGPT](https://nixtla.io/docs/forecasting/special-topics/temporal_hierarchical) | `nixtla-hierarchical-forecast` |
| [Quickstart (TimeGPT-2.1)](https://nixtla.io/docs/forecasting/timegpt_quickstart) | `nixtla-timegpt-forecast`, `nixtla-getting-started` |
| [About TimeGPT](https://nixtla.io/docs/introduction/about_timegpt) | `nixtla-timegpt-forecast` |
| [TimeGPT FAQ](https://nixtla.io/docs/introduction/faq) | `nixtla-timegpt-forecast` |
| [Introduction](https://nixtla.io/docs/introduction/introduction) | `nixtla-timegpt-forecast` |
| [TimeGPT Subscription Plans](https://nixtla.io/docs/introduction/timegpt_subscription_plans) | `nixtla-timegpt-forecast` |
| [Why TimeGPT?](https://nixtla.io/docs/introduction/why_timegpt) | `nixtla-timegpt-forecast` |
| [Asynchronous Jobs](https://nixtla.io/docs/jobs/asynchronous_jobs) | `nixtla-forecast-at-scale` |
| [Date Features](https://nixtla.io/docs/reference/date_features) | `nixtla-exogenous-forecast` |
| [SDK Reference](https://nixtla.io/docs/reference/sdk_reference) | `nixtla-anomaly-detection`, `nixtla-exogenous-forecast`, `nixtla-forecast-at-scale`, `nixtla-forecast-evaluation`, `nixtla-probabilistic-forecast`, `nixtla-scenario-analysis`, `nixtla-timegpt-finetune`, `nixtla-timegpt-forecast`, `nixtla-getting-started` |
| [TimeGPT Excel Add-in (Beta)](https://nixtla.io/docs/reference/timegpt_excel_add_in_beta_) | `nixtla-timegpt-forecast` |
| [TimeGPT in R](https://nixtla.io/docs/reference/timegpt_in_r) | `nixtla-timegpt-forecast` |
| [TimeGEN-1 Quickstart (Azure)](https://nixtla.io/docs/setup/azureai) | `nixtla-timegpt-forecast` |
| [Docker Image for TimeGPT](https://nixtla.io/docs/setup/docker) | `nixtla-timegpt-forecast` |
| [Python Wheel for TimeGPT](https://nixtla.io/docs/setup/python_wheel) | `nixtla-timegpt-forecast` |
| [Setting up your API key](https://nixtla.io/docs/setup/setting_up_your_api_key) | `nixtla-timegpt-forecast`, `nixtla-getting-started` |
| [Forecasting Bitcoin Prices](https://nixtla.io/docs/use_cases/bitcoin_price_prediction) | `nixtla-timegpt-forecast` |
| [Plan Retail Promotions with Coupled Simulation](https://nixtla.io/docs/use_cases/coupled_simulation_retail) | `nixtla-scenario-analysis` |
| [Forecasting Energy Demand](https://nixtla.io/docs/use_cases/forecasting_energy_demand) | `nixtla-timegpt-forecast` |
| [Forecasting Intermittent Demand](https://nixtla.io/docs/use_cases/forecasting_intermittent_demand) | `nixtla-timegpt-forecast` |
| [Forecasting Web Traffic](https://nixtla.io/docs/use_cases/forecasting_web_traffic) | `nixtla-timegpt-forecast` |
| [Logging and Serving with MLFlow](https://nixtla.io/docs/use_cases/logging_and_serving_with_mlflow) | `nixtla-forecast-at-scale` |
| [What-If Forecasting: Price Effects in Retail](https://nixtla.io/docs/use_cases/what_if_forecasting_price_effects_in_retail) | `nixtla-scenario-analysis` |
| [Adapters](https://nixtlaverse.nixtla.io/conformalforecast/adapters.html) | `nixtla-probabilistic-forecast` |
| [Aggregators](https://nixtlaverse.nixtla.io/conformalforecast/aggregators.html) | `nixtla-probabilistic-forecast` |
| [Core contracts](https://nixtlaverse.nixtla.io/conformalforecast/base.html) | `nixtla-probabilistic-forecast` |
| [Capabilities](https://nixtlaverse.nixtla.io/conformalforecast/capabilities.html) | `nixtla-probabilistic-forecast` |
| [Compatibility shims](https://nixtlaverse.nixtla.io/conformalforecast/compat.html) | `nixtla-probabilistic-forecast` |
| [Diagnostics](https://nixtlaverse.nixtla.io/conformalforecast/diagnostics.html) | `nixtla-probabilistic-forecast` |
| [Adapters](https://nixtlaverse.nixtla.io/conformalforecast/docs/adapters/index.html) | `nixtla-probabilistic-forecast` |
| [MLForecast](https://nixtlaverse.nixtla.io/conformalforecast/docs/adapters/mlforecast.html) | `nixtla-probabilistic-forecast` |
| [NeuralForecast](https://nixtlaverse.nixtla.io/conformalforecast/docs/adapters/neuralforecast.html) | `nixtla-probabilistic-forecast` |
| [StatsForecast](https://nixtlaverse.nixtla.io/conformalforecast/docs/adapters/statsforecast.html) | `nixtla-probabilistic-forecast` |
| [Diagnostics](https://nixtlaverse.nixtla.io/conformalforecast/docs/capabilities/diagnostics.html) | `nixtla-probabilistic-forecast` |
| [Exogenous features](https://nixtlaverse.nixtla.io/conformalforecast/docs/capabilities/exogenous.html) | `nixtla-exogenous-forecast`, `nixtla-probabilistic-forecast` |
| [Online updating](https://nixtlaverse.nixtla.io/conformalforecast/docs/capabilities/online-updating.html) | `nixtla-probabilistic-forecast` |
| [Ragged panels](https://nixtlaverse.nixtla.io/conformalforecast/docs/capabilities/ragged-panels.html) | `nixtla-probabilistic-forecast` |
| [Transfer and adaptation](https://nixtlaverse.nixtla.io/conformalforecast/docs/capabilities/transfer.html) | `nixtla-probabilistic-forecast` |
| [Architecture](https://nixtlaverse.nixtla.io/conformalforecast/docs/concepts/architecture.html) | `nixtla-probabilistic-forecast` |
| [Embedding](https://nixtlaverse.nixtla.io/conformalforecast/docs/concepts/embedding.html) | `nixtla-probabilistic-forecast` |
| [Installation](https://nixtlaverse.nixtla.io/conformalforecast/docs/getting-started/installation.html) | `nixtla-probabilistic-forecast` |
| [Quick start](https://nixtlaverse.nixtla.io/conformalforecast/docs/getting-started/quickstart.html) | `nixtla-probabilistic-forecast` |
| [Adaptive conformal inference](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/aci.html) | `nixtla-probabilistic-forecast` |
| [Aggregated adaptive conformal inference](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/agaci.html) | `nixtla-probabilistic-forecast` |
| [Conformalized quantile regression](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/cqr.html) | `nixtla-probabilistic-forecast` |
| [Methods](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/index.html) | `nixtla-probabilistic-forecast` |
| [Nonexchangeable conformal prediction](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/nexcp.html) | `nixtla-probabilistic-forecast` |
| [Sequential predictive conformal inference](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/spci.html) | `nixtla-probabilistic-forecast` |
| [Split conformal](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/split.html) | `nixtla-probabilistic-forecast` |
| [Weighted split conformal](https://nixtlaverse.nixtla.io/conformalforecast/docs/methods/weighted_split.html) | `nixtla-probabilistic-forecast` |
| [conformalforecast](https://nixtlaverse.nixtla.io/conformalforecast/index.html) | `nixtla-probabilistic-forecast` |
| [Methods](https://nixtlaverse.nixtla.io/conformalforecast/methods.html) | `nixtla-probabilistic-forecast` |
| [Nonconformity scores](https://nixtlaverse.nixtla.io/conformalforecast/nonconformity.html) | `nixtla-probabilistic-forecast` |
| [Panel helpers](https://nixtlaverse.nixtla.io/conformalforecast/panel.html) | `nixtla-probabilistic-forecast` |
| [Quantile regressors](https://nixtlaverse.nixtla.io/conformalforecast/quantile_regressors.html) | `nixtla-probabilistic-forecast` |
| [Weighting](https://nixtlaverse.nixtla.io/conformalforecast/weighting.html) | `nixtla-probabilistic-forecast` |
| [Differences](https://nixtlaverse.nixtla.io/coreforecast/differences) | `nixtla-mlforecast` |
| [Expanding](https://nixtlaverse.nixtla.io/coreforecast/expanding) | `nixtla-mlforecast` |
| [Exponentially weighted](https://nixtlaverse.nixtla.io/coreforecast/exponentially_weighted) | `nixtla-mlforecast` |
| [Grouped Array](https://nixtlaverse.nixtla.io/coreforecast/grouped_array) | `nixtla-mlforecast` |
| [coreforecast](https://nixtlaverse.nixtla.io/coreforecast/index) | `nixtla-mlforecast` |
| [Lag transformations - CoreForecast](https://nixtlaverse.nixtla.io/coreforecast/lag_transforms) | `nixtla-mlforecast` |
| [Rolling](https://nixtlaverse.nixtla.io/coreforecast/rolling) | `nixtla-mlforecast` |
| [Scalers](https://nixtlaverse.nixtla.io/coreforecast/scalers) | `nixtla-mlforecast` |
| [Seasonal](https://nixtlaverse.nixtla.io/coreforecast/seasonal) | `nixtla-mlforecast` |
| [Utils](https://nixtlaverse.nixtla.io/coreforecast/utils) | `nixtla-mlforecast` |
| [Favorita](https://nixtlaverse.nixtla.io/datasetsforecast/favorita.html) | `nixtla-forecast-evaluation` |
| [Hierarchical](https://nixtlaverse.nixtla.io/datasetsforecast/hierarchical.html) | `nixtla-forecast-evaluation` |
| [datasetsforecast](https://nixtlaverse.nixtla.io/datasetsforecast/index.html) | `nixtla-forecast-evaluation` |
| [Long Horizon](https://nixtlaverse.nixtla.io/datasetsforecast/long_horizon.html) | `nixtla-forecast-evaluation` |
| [Long-Horizon Original Datasets](https://nixtlaverse.nixtla.io/datasetsforecast/long_horizon2.html) | `nixtla-forecast-evaluation` |
| [M3](https://nixtlaverse.nixtla.io/datasetsforecast/m3.html) | `nixtla-forecast-evaluation` |
| [M4](https://nixtlaverse.nixtla.io/datasetsforecast/m4.html) | `nixtla-forecast-evaluation` |
| [M5](https://nixtlaverse.nixtla.io/datasetsforecast/m5.html) | `nixtla-forecast-evaluation` |
| [PHM2008](https://nixtlaverse.nixtla.io/datasetsforecast/phm2008.html) | `nixtla-forecast-evaluation` |
| [Utils - DatasetsForecast](https://nixtlaverse.nixtla.io/datasetsforecast/utils.html) | `nixtla-forecast-evaluation` |
| [Core - HierarchicalForecast](https://nixtlaverse.nixtla.io/hierarchicalforecast/core.html) | `nixtla-hierarchical-forecast` |
| [Hierarchical Evaluation](https://nixtlaverse.nixtla.io/hierarchicalforecast/evaluation.html) | `nixtla-forecast-evaluation`, `nixtla-hierarchical-forecast` |
| [Bootstrap](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australiandomestictourism-bootstraped-intervals.html) | `nixtla-hierarchical-forecast` |
| [Normality](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australiandomestictourism-intervals.html) | `nixtla-hierarchical-forecast` |
| [Multi-model Aggregation](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australiandomestictourism-multimodel.html) | `nixtla-hierarchical-forecast` |
| [PERMBU](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australiandomestictourism-permbu-intervals.html) | `nixtla-hierarchical-forecast` |
| [Geographical Aggregation (Tourism)](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australiandomestictourism.html) | `nixtla-hierarchical-forecast` |
| [Geographical and Temporal Aggregation (Tourism)](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australiandomestictourismcrosstemporal.html) | `nixtla-hierarchical-forecast` |
| [Temporal Aggregation (Tourism)](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australiandomestictourismtemporal.html) | `nixtla-hierarchical-forecast` |
| [Geographical Aggregation (Prison Population)](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/australianprisonpopulation.html) | `nixtla-hierarchical-forecast` |
| [Exogenous Variables](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/exogenousvariables.html) | `nixtla-exogenous-forecast`, `nixtla-hierarchical-forecast` |
| [Hierarchical Forecasting at Scale](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/hierarchicalforecastingatscale.html) | `nixtla-forecast-at-scale`, `nixtla-hierarchical-forecast` |
| [Tutorials](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/index.html) | `nixtla-hierarchical-forecast` |
| [Install - HierarchicalForecast](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/installation.html) | `nixtla-hierarchical-forecast` |
| [Introduction](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/introduction.html) | `nixtla-hierarchical-forecast` |
| [Local vs Global Temporal Aggregation](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/localglobalaggregation.html) | `nixtla-hierarchical-forecast` |
| [Temporal Aggregation with THIEF](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/m3withthief.html) | `nixtla-hierarchical-forecast` |
| [Neural/MLForecast](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/mlframeworksexample.html) | `nixtla-hierarchical-forecast` |
| [Non-Negative MinTrace](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/nonnegativereconciliation.html) | `nixtla-hierarchical-forecast` |
| [Probabilistic Reconciliation Methods Comparison](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/probabilistic-reconciliation-comparison.html) | `nixtla-hierarchical-forecast`, `nixtla-probabilistic-forecast` |
| [Reconciliation Diagnostics](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/reconciliationdiagnostics.html) | `nixtla-hierarchical-forecast` |
| [Probabilistic Forecast Evaluation](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/tourismlarge-evaluation.html) | `nixtla-forecast-evaluation`, `nixtla-hierarchical-forecast` |
| [Quick Start - HierarchicalForecast](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/tourismsmall.html) | `nixtla-hierarchical-forecast` |
| [Quick Start (Polars)](https://nixtlaverse.nixtla.io/hierarchicalforecast/examples/tourismsmallpolars.html) | `nixtla-hierarchical-forecast` |
| [Hierarchical Forecast 👑](https://nixtlaverse.nixtla.io/hierarchicalforecast/index.html) | `nixtla-hierarchical-forecast` |
| [Reconciliation Methods](https://nixtlaverse.nixtla.io/hierarchicalforecast/methods.html) | `nixtla-hierarchical-forecast` |
| [Probabilistic Methods](https://nixtlaverse.nixtla.io/hierarchicalforecast/probabilistic_methods.html) | `nixtla-hierarchical-forecast`, `nixtla-probabilistic-forecast` |
| [Aggregation/Visualization Utils](https://nixtlaverse.nixtla.io/hierarchicalforecast/utils.html) | `nixtla-hierarchical-forecast` |
| [Nixtlaverse](https://nixtlaverse.nixtla.io/index) | `nixtla-timegpt-forecast`, `nixtla-getting-started` |
| [Auto](https://nixtlaverse.nixtla.io/mlforecast/auto.html) | `nixtla-mlforecast` |
| [Callbacks](https://nixtlaverse.nixtla.io/mlforecast/callbacks.html) | `nixtla-mlforecast` |
| [Conformal Prediction](https://nixtlaverse.nixtla.io/mlforecast/conformal_prediction.html) | `nixtla-mlforecast`, `nixtla-probabilistic-forecast` |
| [Core - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/core.html) | `nixtla-mlforecast` |
| [Distributed Forecast](https://nixtlaverse.nixtla.io/mlforecast/distributed.forecast.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [DaskLGBMForecast](https://nixtlaverse.nixtla.io/mlforecast/distributed.models.dask.lgb.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [DaskXGBForecast](https://nixtlaverse.nixtla.io/mlforecast/distributed.models.dask.xgb.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [RayLGBMForecast](https://nixtlaverse.nixtla.io/mlforecast/distributed.models.ray.lgb.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [RayXGBForecast](https://nixtlaverse.nixtla.io/mlforecast/distributed.models.ray.xgb.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [SparkLGBMForecast](https://nixtlaverse.nixtla.io/mlforecast/distributed.models.spark.lgb.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [SparkXGBForecast](https://nixtlaverse.nixtla.io/mlforecast/distributed.models.spark.xgb.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [End to end walkthrough - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/getting-started/end_to_end_walkthrough.html) | `nixtla-mlforecast` |
| [Install - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/getting-started/install.html) | `nixtla-mlforecast` |
| [Quick start (distributed)](https://nixtlaverse.nixtla.io/mlforecast/docs/getting-started/quick_start_distributed.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [Quick start (local)](https://nixtlaverse.nixtla.io/mlforecast/docs/getting-started/quick_start_local.html) | `nixtla-mlforecast`, `nixtla-getting-started` |
| [Analyzing the trained models](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/analyzing_models.html) | `nixtla-mlforecast` |
| [Cross validation - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/cross_validation.html) | `nixtla-forecast-evaluation`, `nixtla-mlforecast` |
| [Custom date features](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/custom_date_features.html) | `nixtla-exogenous-forecast`, `nixtla-mlforecast` |
| [Custom training](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/custom_training.html) | `nixtla-mlforecast` |
| [Exogenous features](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/exogenous_features.html) | `nixtla-exogenous-forecast`, `nixtla-mlforecast` |
| [Hyperparameter optimization - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/hyperparameter_optimization.html) | `nixtla-mlforecast` |
| [Lag transformations - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/lag_transforms_guide.html) | `nixtla-mlforecast` |
| [MLflow - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/mlflow.html) | `nixtla-forecast-at-scale`, `nixtla-mlforecast` |
| [One model per step](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/one_model_per_horizon.html) | `nixtla-mlforecast` |
| [Pooled lag transforms](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/pooled_lag_transforms.html) | `nixtla-mlforecast` |
| [Predict callbacks](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/predict_callbacks.html) | `nixtla-mlforecast` |
| [Predicting a subset of ids](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/predict_subset.html) | `nixtla-mlforecast` |
| [Probabilistic forecasting - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/prediction_intervals.html) | `nixtla-mlforecast`, `nixtla-probabilistic-forecast` |
| [Sample weights](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/sample_weights.html) | `nixtla-mlforecast` |
| [Using scikit-learn pipelines](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/sklearn_pipelines.html) | `nixtla-mlforecast` |
| [Target transformations](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/target_transforms_guide.html) | `nixtla-mlforecast` |
| [Training with numpy arrays](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/training_with_numpy.html) | `nixtla-mlforecast` |
| [Transfer Learning - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/transfer_learning.html) | `nixtla-mlforecast` |
| [Transforming exogenous features](https://nixtlaverse.nixtla.io/mlforecast/docs/how-to-guides/transforming_exog.html) | `nixtla-mlforecast` |
| [Electricity Load Forecast - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/tutorials/electricity_load_forecasting.html) | `nixtla-mlforecast` |
| [Detect Demand Peaks - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/docs/tutorials/electricity_peak_forecasting.html) | `nixtla-mlforecast` |
| [Incremental Forecast generation](https://nixtlaverse.nixtla.io/mlforecast/docs/tutorials/incremental_forecasting.html) | `nixtla-mlforecast` |
| [M4 Competition](https://nixtlaverse.nixtla.io/mlforecast/docs/tutorials/m4.html) | `nixtla-mlforecast` |
| [Prediction intervals](https://nixtlaverse.nixtla.io/mlforecast/docs/tutorials/prediction_intervals_in_forecasting_models.html) | `nixtla-mlforecast`, `nixtla-probabilistic-forecast` |
| [Transfer Conformal Prediction Intervals](https://nixtlaverse.nixtla.io/mlforecast/docs/tutorials/transfer_conformal_prediction.html) | `nixtla-mlforecast`, `nixtla-probabilistic-forecast` |
| [Feature engineering - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/feature_engineering.html) | `nixtla-exogenous-forecast`, `nixtla-mlforecast` |
| [MLForecast](https://nixtlaverse.nixtla.io/mlforecast/forecast.html) | `nixtla-mlforecast` |
| [Grouped Array](https://nixtlaverse.nixtla.io/mlforecast/grouped_array) | `nixtla-mlforecast` |
| [Machine Learning 🤖 Forecast](https://nixtlaverse.nixtla.io/mlforecast/index.html) | `nixtla-mlforecast` |
| [Lag transforms](https://nixtlaverse.nixtla.io/mlforecast/lag_transforms.html) | `nixtla-mlforecast` |
| [LightGBMCV](https://nixtlaverse.nixtla.io/mlforecast/lgb_cv.html) | `nixtla-mlforecast` |
| [Optimization](https://nixtlaverse.nixtla.io/mlforecast/optimization.html) | `nixtla-mlforecast` |
| [Target transforms](https://nixtlaverse.nixtla.io/mlforecast/target_transforms.html) | `nixtla-mlforecast` |
| [Utils - MLForecast](https://nixtlaverse.nixtla.io/mlforecast/utils.html) | `nixtla-mlforecast` |
| [Hyperparameter Optimization - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/common.base_auto.html) | `nixtla-neuralforecast` |
| [NN Modules](https://nixtlaverse.nixtla.io/neuralforecast/common.modules.html) | `nixtla-neuralforecast` |
| [TemporalNorm](https://nixtlaverse.nixtla.io/neuralforecast/common.scalers.html) | `nixtla-neuralforecast` |
| [Core - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/core.html) | `nixtla-neuralforecast` |
| [NeuralForecast Map](https://nixtlaverse.nixtla.io/neuralforecast/docs/api-reference/neuralforecast_map.html) | `nixtla-neuralforecast` |
| [Categorical features](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/categorical_features.html) | `nixtla-exogenous-forecast`, `nixtla-neuralforecast` |
| [NeuralForecast Cross Validation API and Parameters](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/cross_validation.html) | `nixtla-forecast-evaluation`, `nixtla-neuralforecast` |
| [Exogenous Variables](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/exogenous_variables.html) | `nixtla-exogenous-forecast`, `nixtla-neuralforecast` |
| [Hyperparameter Optimization - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/hyperparameter_tuning.html) | `nixtla-neuralforecast` |
| [Optimization Objectives](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/objectives.html) | `nixtla-neuralforecast` |
| [Forecasting Models](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/overview.html) | `nixtla-neuralforecast` |
| [Predict Insample](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/predictInsample.html) | `nixtla-neuralforecast` |
| [Save and Load Models](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/save_load_models.html) | `nixtla-neuralforecast` |
| [Time Series Scaling](https://nixtlaverse.nixtla.io/neuralforecast/docs/capabilities/time_series_scaling.html) | `nixtla-neuralforecast` |
| [Data Requirements](https://nixtlaverse.nixtla.io/neuralforecast/docs/getting-started/datarequirements.html) | `nixtla-neuralforecast`, `nixtla-time-series-data` |
| [Installation](https://nixtlaverse.nixtla.io/neuralforecast/docs/getting-started/installation.html) | `nixtla-neuralforecast` |
| [About NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/getting-started/introduction.html) | `nixtla-neuralforecast` |
| [Quickstart](https://nixtlaverse.nixtla.io/neuralforecast/docs/getting-started/quickstart.html) | `nixtla-neuralforecast`, `nixtla-getting-started` |
| [Adding Models to NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/adding_models.html) | `nixtla-neuralforecast` |
| [Statistical, Machine Learning and Neural Forecasting methods- NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/comparing_methods.html) | `nixtla-forecast-evaluation`, `nixtla-neuralforecast` |
| [Modify the configure_optimizers() behavior of NeuralForecast models](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/configure_optimizers.html) | `nixtla-neuralforecast` |
| [Uncertainty quantification with Conformal Prediction](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/conformal_prediction.html) | `nixtla-neuralforecast`, `nixtla-probabilistic-forecast` |
| [Converting Models to ONNX](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/converting_onnx.html) | `nixtla-forecast-at-scale`, `nixtla-neuralforecast` |
| [Time Series Cross Validation Tutorial with NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/cross_validation.html) | `nixtla-forecast-evaluation`, `nixtla-neuralforecast` |
| [Distributed Training](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/distributed_neuralforecast.html) | `nixtla-forecast-at-scale`, `nixtla-neuralforecast` |
| [Explainability for Deep Learning Forecasting Models](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/explainability.html) | `nixtla-neuralforecast`, `nixtla-scenario-analysis` |
| [Forecasting with TFT: Temporal Fusion Transformer](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/forecasting_tft.html) | `nixtla-neuralforecast` |
| [End to End Walkthrough - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/getting_started_complete.html) | `nixtla-neuralforecast` |
| [Hierarchical Forecast - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/hierarchical_forecasting.html) | `nixtla-hierarchical-forecast`, `nixtla-neuralforecast` |
| [Intermittent Data](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/intermittent_data.html) | `nixtla-neuralforecast` |
| [Interpretable Decompositions](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/interpretable_decompositions.html) | `nixtla-neuralforecast`, `nixtla-scenario-analysis` |
| [Using Large Datasets](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/large_datasets.html) | `nixtla-forecast-at-scale`, `nixtla-neuralforecast` |
| [Long-Horizon Forecasting with NHITS](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/longhorizon_nhits.html) | `nixtla-neuralforecast` |
| [Long-Horizon Probabilistic Forecasting](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/longhorizon_probabilistic.html) | `nixtla-neuralforecast`, `nixtla-probabilistic-forecast` |
| [Long-Horizon Forecasting with Transformer models](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/longhorizon_transformers.html) | `nixtla-neuralforecast` |
| [Multivariate Forecasting with TSMixer](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/multivariate_tsmixer.html) | `nixtla-neuralforecast` |
| [Robust Forecasting](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/robust_forecasting.html) | `nixtla-neuralforecast` |
| [Simulation Paths - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/simulation.html) | `nixtla-neuralforecast`, `nixtla-scenario-analysis` |
| [Temporal Classification](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/temporal_classification.html) | `nixtla-neuralforecast` |
| [Transfer Learning - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/transfer_learning.html) | `nixtla-neuralforecast` |
| [Probabilistic Forecasting - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/uncertainty_quantification.html) | `nixtla-neuralforecast`, `nixtla-probabilistic-forecast` |
| [Using MLflow](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/using_mlflow.html) | `nixtla-forecast-at-scale`, `nixtla-neuralforecast` |
| [Weighting Timesteps - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/tutorials/weighting_timesteps.html) | `nixtla-neuralforecast` |
| [Detect Demand Peaks - NeuralForecast](https://nixtlaverse.nixtla.io/neuralforecast/docs/use-cases/electricity_peak_forecasting.html) | `nixtla-neuralforecast` |
| [Predictive Maintenance](https://nixtlaverse.nixtla.io/neuralforecast/docs/use-cases/predictive_maintenance.html) | `nixtla-neuralforecast` |
| [NumPy Evaluation](https://nixtlaverse.nixtla.io/neuralforecast/losses.numpy.html) | `nixtla-neuralforecast`, `nixtla-probabilistic-forecast` |
| [PyTorch Losses](https://nixtlaverse.nixtla.io/neuralforecast/losses.pytorch.html) | `nixtla-neuralforecast`, `nixtla-probabilistic-forecast` |
| [Autoformer](https://nixtlaverse.nixtla.io/neuralforecast/models.autoformer.html) | `nixtla-neuralforecast` |
| [BiTCN](https://nixtlaverse.nixtla.io/neuralforecast/models.bitcn.html) | `nixtla-neuralforecast` |
| [DeepAR](https://nixtlaverse.nixtla.io/neuralforecast/models.deepar.html) | `nixtla-neuralforecast` |
| [DeepNPTS](https://nixtlaverse.nixtla.io/neuralforecast/models.deepnpts.html) | `nixtla-neuralforecast` |
| [Dilated RNN](https://nixtlaverse.nixtla.io/neuralforecast/models.dilated_rnn.html) | `nixtla-neuralforecast` |
| [DLinear](https://nixtlaverse.nixtla.io/neuralforecast/models.dlinear.html) | `nixtla-neuralforecast` |
| [FEDformer](https://nixtlaverse.nixtla.io/neuralforecast/models.fedformer.html) | `nixtla-neuralforecast` |
| [GRU](https://nixtlaverse.nixtla.io/neuralforecast/models.gru.html) | `nixtla-neuralforecast` |
| [HINT](https://nixtlaverse.nixtla.io/neuralforecast/models.hint.html) | `nixtla-neuralforecast` |
| [Automatic Forecasting](https://nixtlaverse.nixtla.io/neuralforecast/models.html) | `nixtla-neuralforecast` |
| [Informer Time Series Forecasting in Python](https://nixtlaverse.nixtla.io/neuralforecast/models.informer.html) | `nixtla-neuralforecast` |
| [iTransformer Time Series Forecasting in Python](https://nixtlaverse.nixtla.io/neuralforecast/models.itransformer.html) | `nixtla-neuralforecast` |
| [KAN Time Series Forecasting in Python](https://nixtlaverse.nixtla.io/neuralforecast/models.kan.html) | `nixtla-neuralforecast` |
| [LSTM](https://nixtlaverse.nixtla.io/neuralforecast/models.lstm.html) | `nixtla-neuralforecast` |
| [MLP](https://nixtlaverse.nixtla.io/neuralforecast/models.mlp.html) | `nixtla-neuralforecast` |
| [MLPMultivariate](https://nixtlaverse.nixtla.io/neuralforecast/models.mlpmultivariate.html) | `nixtla-neuralforecast` |
| [NBEATS](https://nixtlaverse.nixtla.io/neuralforecast/models.nbeats.html) | `nixtla-neuralforecast` |
| [NBEATSx](https://nixtlaverse.nixtla.io/neuralforecast/models.nbeatsx.html) | `nixtla-neuralforecast` |
| [NHITS](https://nixtlaverse.nixtla.io/neuralforecast/models.nhits.html) | `nixtla-neuralforecast` |
| [NLinear](https://nixtlaverse.nixtla.io/neuralforecast/models.nlinear.html) | `nixtla-neuralforecast` |
| [PatchTST Time Series Forecasting in Python](https://nixtlaverse.nixtla.io/neuralforecast/models.patchtst.html) | `nixtla-neuralforecast` |
| [Reversible Mixture of KAN - RMoK](https://nixtlaverse.nixtla.io/neuralforecast/models.rmok.html) | `nixtla-neuralforecast` |
| [RNN](https://nixtlaverse.nixtla.io/neuralforecast/models.rnn.html) | `nixtla-neuralforecast` |
| [SOFTS](https://nixtlaverse.nixtla.io/neuralforecast/models.softs.html) | `nixtla-neuralforecast` |
| [SOFTSSharp](https://nixtlaverse.nixtla.io/neuralforecast/models.softssharp.html) | `nixtla-neuralforecast` |
| [StemGNN](https://nixtlaverse.nixtla.io/neuralforecast/models.stemgnn.html) | `nixtla-neuralforecast` |
| [TCN](https://nixtlaverse.nixtla.io/neuralforecast/models.tcn.html) | `nixtla-neuralforecast` |
| [Temporal Fusion Transformer Forecasting in Python](https://nixtlaverse.nixtla.io/neuralforecast/models.tft.html) | `nixtla-neuralforecast` |
| [TiDE](https://nixtlaverse.nixtla.io/neuralforecast/models.tide.html) | `nixtla-neuralforecast` |
| [Time-LLM](https://nixtlaverse.nixtla.io/neuralforecast/models.timellm.html) | `nixtla-neuralforecast` |
| [TimeMixer](https://nixtlaverse.nixtla.io/neuralforecast/models.timemixer.html) | `nixtla-neuralforecast` |
| [TimesNet](https://nixtlaverse.nixtla.io/neuralforecast/models.timesnet.html) | `nixtla-neuralforecast` |
| [TimeXer](https://nixtlaverse.nixtla.io/neuralforecast/models.timexer.html) | `nixtla-neuralforecast` |
| [TSMixer](https://nixtlaverse.nixtla.io/neuralforecast/models.tsmixer.html) | `nixtla-neuralforecast` |
| [TSMixerx](https://nixtlaverse.nixtla.io/neuralforecast/models.tsmixerx.html) | `nixtla-neuralforecast` |
| [Vanilla Transformer](https://nixtlaverse.nixtla.io/neuralforecast/models.vanillatransformer.html) | `nixtla-neuralforecast` |
| [XLinear](https://nixtlaverse.nixtla.io/neuralforecast/models.xlinear.html) | `nixtla-neuralforecast` |
| [xLSTM](https://nixtlaverse.nixtla.io/neuralforecast/models.xlstm.html) | `nixtla-neuralforecast` |
| [PyTorch Dataset/Loader](https://nixtlaverse.nixtla.io/neuralforecast/tsdataset.html) | `nixtla-neuralforecast` |
| [Example Data](https://nixtlaverse.nixtla.io/neuralforecast/utils.html) | `nixtla-neuralforecast` |
| [Contribute to Nixtla](https://nixtlaverse.nixtla.io/statsforecast/docs/contribute/contribute.html) | Context only: company/legal/contributor information |
| [Nixtla Documentation](https://nixtlaverse.nixtla.io/statsforecast/docs/contribute/docs.html) | Context only: company/legal/contributor information |
| [Understanding Issue Labels](https://nixtlaverse.nixtla.io/statsforecast/docs/contribute/issue-labels.html) | Context only: company/legal/contributor information |
| [Submit an Issue 📢](https://nixtlaverse.nixtla.io/statsforecast/docs/contribute/issues.html) | Context only: company/legal/contributor information |
| [Step-by-step Contribution Guide](https://nixtlaverse.nixtla.io/statsforecast/docs/contribute/step-by-step.html) | Context only: company/legal/contributor information |
| [Contributing Code to Nixtla Development](https://nixtlaverse.nixtla.io/statsforecast/docs/contribute/techstack.html) | Context only: company/legal/contributor information |
| [Dask](https://nixtlaverse.nixtla.io/statsforecast/docs/distributed/dask.html) | `nixtla-forecast-at-scale`, `nixtla-statsforecast` |
| [Ray](https://nixtlaverse.nixtla.io/statsforecast/docs/distributed/ray.html) | `nixtla-forecast-at-scale`, `nixtla-statsforecast` |
| [Spark](https://nixtlaverse.nixtla.io/statsforecast/docs/distributed/spark.html) | `nixtla-forecast-at-scale`, `nixtla-statsforecast` |
| [Amazon Forecast vs StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/experiments/amazonstatsforecast.html) | `nixtla-statsforecast` |
| [AutoARIMA Comparison (Prophet and pmdarima)](https://nixtlaverse.nixtla.io/statsforecast/docs/experiments/autoarima_vs_prophet.html) | `nixtla-statsforecast` |
| [AutoARIMAProphet Adapter](https://nixtlaverse.nixtla.io/statsforecast/docs/experiments/autoarimaprophet_adapter.html) | `nixtla-statsforecast` |
| [Forecasting at Scale using ETS and ray (M5)](https://nixtlaverse.nixtla.io/statsforecast/docs/experiments/ets_ray_m5.html) | `nixtla-statsforecast` |
| [StatsForecast ETS and Facebook Prophet on Spark (M5)](https://nixtlaverse.nixtla.io/statsforecast/docs/experiments/prophet_spark_m5.html) | `nixtla-statsforecast` |
| [End to End Walkthrough - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/getting-started/getting_started_complete.html) | `nixtla-statsforecast` |
| [End to End Walkthrough with Polars](https://nixtlaverse.nixtla.io/statsforecast/docs/getting-started/getting_started_complete_polars.html) | `nixtla-statsforecast` |
| [Quick Start - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/getting-started/getting_started_short.html) | `nixtla-statsforecast`, `nixtla-getting-started` |
| [Install - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/getting-started/installation.html) | `nixtla-statsforecast` |
| [Automatic Time Series Forecasting](https://nixtlaverse.nixtla.io/statsforecast/docs/how-to-guides/automatic_forecasting.html) | `nixtla-statsforecast` |
| [Exogenous Regressors](https://nixtlaverse.nixtla.io/statsforecast/docs/how-to-guides/exogenous.html) | `nixtla-exogenous-forecast`, `nixtla-statsforecast` |
| [Generating features](https://nixtlaverse.nixtla.io/statsforecast/docs/how-to-guides/generating_features.html) | `nixtla-exogenous-forecast`, `nixtla-statsforecast` |
| [Numba caching](https://nixtlaverse.nixtla.io/statsforecast/docs/how-to-guides/numba_cache.html) | `nixtla-statsforecast` |
| [Sklearn models](https://nixtlaverse.nixtla.io/statsforecast/docs/how-to-guides/sklearn_models.html) | `nixtla-statsforecast` |
| [ADIDA Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/adida.html) | `nixtla-statsforecast` |
| [ARCH Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/arch.html) | `nixtla-statsforecast` |
| [ARIMA Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/arima.html) | `nixtla-statsforecast` |
| [AutoARIMA Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/autoarima.html) | `nixtla-statsforecast` |
| [AutoCES Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/autoces.html) | `nixtla-statsforecast` |
| [AutoETS Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/autoets.html) | `nixtla-statsforecast` |
| [AutoRegressive Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/autoregressive.html) | `nixtla-statsforecast` |
| [AutoTheta Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/autotheta.html) | `nixtla-statsforecast` |
| [Conformal Seasonal Pool (CSP)](https://nixtlaverse.nixtla.io/statsforecast/docs/models/conformalseasonalpool.html) | `nixtla-probabilistic-forecast`, `nixtla-statsforecast` |
| [CrostonClassic Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/crostonclassic.html) | `nixtla-statsforecast` |
| [CrostonOptimized Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/crostonoptimized.html) | `nixtla-statsforecast` |
| [CrostonSBA Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/crostonsba.html) | `nixtla-statsforecast` |
| [Dynamic Optimized Theta Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/dynamicoptimizedtheta.html) | `nixtla-statsforecast` |
| [Dynamic Standard Theta Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/dynamicstandardtheta.html) | `nixtla-statsforecast` |
| [GARCH Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/garch.html) | `nixtla-statsforecast` |
| [Holt Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/holt.html) | `nixtla-statsforecast` |
| [Holt Winters Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/holtwinters.html) | `nixtla-statsforecast` |
| [IMAPA Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/imapa.html) | `nixtla-statsforecast` |
| [MFLES](https://nixtlaverse.nixtla.io/statsforecast/docs/models/mfles.html) | `nixtla-statsforecast` |
| [Multiple Seasonal Trend (MSTL)](https://nixtlaverse.nixtla.io/statsforecast/docs/models/multipleseasonaltrend.html) | `nixtla-statsforecast` |
| [Optimized Theta Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/optimizedtheta.html) | `nixtla-statsforecast` |
| [Seasonal Exponential Smoothing Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/seasonalexponentialsmoothing.html) | `nixtla-statsforecast` |
| [Seasonal Exponential Smoothing Optimized Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/seasonalexponentialsmoothingoptimized.html) | `nixtla-statsforecast` |
| [Simple Exponential Smoothing Optimized Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/simpleexponentialoptimized.html) | `nixtla-statsforecast` |
| [Simple Exponential Smoothing Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/simpleexponentialsmoothing.html) | `nixtla-statsforecast` |
| [Standard Theta Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/standardtheta.html) | `nixtla-statsforecast` |
| [TSB Model](https://nixtlaverse.nixtla.io/statsforecast/docs/models/tsb.html) | `nixtla-statsforecast` |
| [Anomaly Detection](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/anomalydetection.html) | `nixtla-anomaly-detection`, `nixtla-statsforecast` |
| [Conformal Prediction](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/conformalprediction.html) | `nixtla-probabilistic-forecast`, `nixtla-statsforecast` |
| [Cross validation - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/crossvalidation.html) | `nixtla-forecast-evaluation`, `nixtla-statsforecast` |
| [Electricity Load Forecast - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/electricityloadforecasting.html) | `nixtla-statsforecast` |
| [Detect Demand Peaks - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/electricitypeakforecasting.html) | `nixtla-statsforecast` |
| [Volatility forecasting (GARCH & ARCH)](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/garch_tutorial.html) | `nixtla-statsforecast` |
| [Intermittent or Sparse Data](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/intermittentdata.html) | `nixtla-statsforecast` |
| [MLFlow - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/mlflow.html) | `nixtla-forecast-at-scale`, `nixtla-statsforecast` |
| [Multiple seasonalities](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/multipleseasonalities.html) | `nixtla-statsforecast` |
| [Trajectory Simulation](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/simulation.html) | `nixtla-scenario-analysis`, `nixtla-statsforecast` |
| [Statistical, Machine Learning and Neural Forecasting methods - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/statisticalneuralmethods.html) | `nixtla-forecast-evaluation`, `nixtla-statsforecast` |
| [Probabilistic Forecasting - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/docs/tutorials/uncertaintyintervals.html) | `nixtla-probabilistic-forecast`, `nixtla-statsforecast` |
| [Statistical ⚡️ Forecast](https://nixtlaverse.nixtla.io/statsforecast/index.html) | `nixtla-statsforecast` |
| [Core Methods](https://nixtlaverse.nixtla.io/statsforecast/src/core/core.html) | `nixtla-statsforecast` |
| [Fugue Backend](https://nixtlaverse.nixtla.io/statsforecast/src/core/distributed.fugue.html) | `nixtla-forecast-at-scale`, `nixtla-statsforecast` |
| [Models](https://nixtlaverse.nixtla.io/statsforecast/src/core/models.html) | `nixtla-statsforecast` |
| [StatsForecast's Models](https://nixtlaverse.nixtla.io/statsforecast/src/core/models_intro.html) | `nixtla-statsforecast` |
| [Feature engineering - StatsForecast](https://nixtlaverse.nixtla.io/statsforecast/src/feature_engineering.html) | `nixtla-exogenous-forecast`, `nixtla-statsforecast` |
| [Generation and Composition](https://nixtlaverse.nixtla.io/synforecast/composition.html) | `nixtla-synthetic-data` |
| [BaseGenerator](https://nixtlaverse.nixtla.io/synforecast/core.html) | `nixtla-synthetic-data` |
| [Dataset](https://nixtlaverse.nixtla.io/synforecast/dataset.html) | `nixtla-synthetic-data` |
| [Anomaly injection](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/anomalies.html) | `nixtla-synthetic-data` |
| [SynAugment: data augmentation](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/augmentation.html) | `nixtla-synthetic-data` |
| [Data augmentation with real datasets](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/augmentation_real_data.html) | `nixtla-synthetic-data` |
| [Interpretable pool](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/balanced_pool.html) | `nixtla-synthetic-data` |
| [Changepoint injection](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/changepoints.html) | `nixtla-synthetic-data` |
| [Write your own generator](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/custom_generator.html) | `nixtla-synthetic-data` |
| [Compose datasets with SynSet](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/dataset.html) | `nixtla-synthetic-data` |
| [Exogenous variables](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/exogenous.html) | `nixtla-exogenous-forecast`, `nixtla-synthetic-data` |
| [Feature-space coverage of the generator pools](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/feature_coverage.html) | `nixtla-synthetic-data` |
| [Missing data patterns](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/missingness.html) | `nixtla-synthetic-data` |
| [Multivariate missing data](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/multivariate_missingness.html) | `nixtla-synthetic-data` |
| [Multivariatize a univariate generator](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/multivariatize.html) | `nixtla-synthetic-data` |
| [Non-parametric augmentation](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/nonparametric_augmentation.html) | `nixtla-synthetic-data` |
| [Robustness testing with known ground truth](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/robustness_testing.html) | `nixtla-synthetic-data` |
| [When does synthetic data help?](https://nixtlaverse.nixtla.io/synforecast/docs/capabilities/when_synthetic_helps.html) | `nixtla-synthetic-data` |
| [Clickstream](https://nixtlaverse.nixtla.io/synforecast/docs/generators/domain/clickstream.html) | `nixtla-synthetic-data` |
| [Daily active users](https://nixtlaverse.nixtla.io/synforecast/docs/generators/domain/daily_active_users.html) | `nixtla-synthetic-data` |
| [Energy load](https://nixtlaverse.nixtla.io/synforecast/docs/generators/domain/energy_load.html) | `nixtla-synthetic-data` |
| [Intermittent demand](https://nixtlaverse.nixtla.io/synforecast/docs/generators/domain/intermittent_demand.html) | `nixtla-synthetic-data` |
| [IoT sensor](https://nixtlaverse.nixtla.io/synforecast/docs/generators/domain/iot_sensor.html) | `nixtla-synthetic-data` |
| [State space](https://nixtlaverse.nixtla.io/synforecast/docs/generators/domain/state_space.html) | `nixtla-synthetic-data` |
| [Vital signs](https://nixtlaverse.nixtla.io/synforecast/docs/generators/domain/vital_signs.html) | `nixtla-synthetic-data` |
| [Copula (dependency structure)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/multivariate/copula.html) | `nixtla-synthetic-data` |
| [Gaussian process (kernel-defined structure)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/multivariate/gaussian_process.html) | `nixtla-synthetic-data` |
| [VAR (vector autoregression)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/multivariate/var.html) | `nixtla-synthetic-data` |
| [KernelSynth](https://nixtlaverse.nixtla.io/synforecast/docs/generators/pretraining/kernel_synth.html) | `nixtla-synthetic-data` |
| [MAR](https://nixtlaverse.nixtla.io/synforecast/docs/generators/pretraining/mar.html) | `nixtla-synthetic-data` |
| [Temporal causal model](https://nixtlaverse.nixtla.io/synforecast/docs/generators/pretraining/tcm.html) | `nixtla-synthetic-data` |
| [TSI](https://nixtlaverse.nixtla.io/synforecast/docs/generators/pretraining/tsi.html) | `nixtla-synthetic-data` |
| [ETS (exponential smoothing)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/statistical/ets.html) | `nixtla-synthetic-data` |
| [INAR (integer counts)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/statistical/inar.html) | `nixtla-synthetic-data` |
| [Random walk](https://nixtlaverse.nixtla.io/synforecast/docs/generators/statistical/random_walk.html) | `nixtla-synthetic-data` |
| [SARIMA](https://nixtlaverse.nixtla.io/synforecast/docs/generators/statistical/sarima.html) | `nixtla-synthetic-data` |
| [Seasonal](https://nixtlaverse.nixtla.io/synforecast/docs/generators/statistical/seasonal.html) | `nixtla-synthetic-data` |
| [Bounded process (proportions and rates)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/bounded_process.html) | `nixtla-synthetic-data` |
| [Chaotic systems](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/chaotic_system.html) | `nixtla-synthetic-data` |
| [Cyclic (irregular cycles)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/cyclic.html) | `nixtla-synthetic-data` |
| [Fractional Brownian motion (long memory)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/fractional_brownian_motion.html) | `nixtla-synthetic-data` |
| [GARCH (volatility clustering)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/garch.html) | `nixtla-synthetic-data` |
| [Geometric Brownian motion](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/geometric_brownian_motion.html) | `nixtla-synthetic-data` |
| [Hawkes process (self-excitation)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/hawkes_process.html) | `nixtla-synthetic-data` |
| [Jump diffusion](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/jump_diffusion.html) | `nixtla-synthetic-data` |
| [Levy process (heavy tails)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/levy_process.html) | `nixtla-synthetic-data` |
| [Ornstein-Uhlenbeck (mean reversion)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/ornstein_uhlenbeck.html) | `nixtla-synthetic-data` |
| [Poisson process (event arrivals)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/poisson_process.html) | `nixtla-synthetic-data` |
| [Regime switching (Markov switching)](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/regime_switching.html) | `nixtla-synthetic-data` |
| [Stochastic volatility](https://nixtlaverse.nixtla.io/synforecast/docs/generators/stochastic/stochastic_volatility.html) | `nixtla-synthetic-data` |
| [Installation](https://nixtlaverse.nixtla.io/synforecast/docs/getting-started/installation.html) | `nixtla-synthetic-data` |
| [Quick start](https://nixtlaverse.nixtla.io/synforecast/docs/getting-started/quickstart.html) | `nixtla-synthetic-data` |
| [MLForecast with synthetic data](https://nixtlaverse.nixtla.io/synforecast/docs/integrations/mlforecast.html) | `nixtla-synthetic-data` |
| [NeuralForecast with synthetic data](https://nixtlaverse.nixtla.io/synforecast/docs/integrations/neuralforecast.html) | `nixtla-synthetic-data` |
| [Works with the Nixtlaverse](https://nixtlaverse.nixtla.io/synforecast/docs/integrations/nixtlaverse.html) | `nixtla-synthetic-data` |
| [StatsForecast with synthetic data](https://nixtlaverse.nixtla.io/synforecast/docs/integrations/statsforecast.html) | `nixtla-synthetic-data` |
| [Corpus evaluation](https://nixtlaverse.nixtla.io/synforecast/evaluation.html) | `nixtla-forecast-evaluation`, `nixtla-synthetic-data` |
| [Exogenous Variables](https://nixtlaverse.nixtla.io/synforecast/exogenous.html) | `nixtla-exogenous-forecast`, `nixtla-synthetic-data` |
| [Domain-Specific Generators](https://nixtlaverse.nixtla.io/synforecast/generators_domain.html) | `nixtla-synthetic-data` |
| [Multivariate Generators](https://nixtlaverse.nixtla.io/synforecast/generators_multivariate.html) | `nixtla-synthetic-data` |
| [Pretraining Generators](https://nixtlaverse.nixtla.io/synforecast/generators_pretraining.html) | `nixtla-synthetic-data` |
| [Statistical Generators](https://nixtlaverse.nixtla.io/synforecast/generators_statistical.html) | `nixtla-synthetic-data` |
| [Stochastic Generators](https://nixtlaverse.nixtla.io/synforecast/generators_stochastic.html) | `nixtla-synthetic-data` |
| [Synthetic 🧬 Forecast](https://nixtlaverse.nixtla.io/synforecast/index.html) | `nixtla-synthetic-data` |
| [Data](https://nixtlaverse.nixtla.io/utilsforecast/data.html) | `nixtla-forecast-evaluation`, `nixtla-time-series-data` |
| [Multi-Objective Model Selection with Pareto Frontier](https://nixtlaverse.nixtla.io/utilsforecast/docs/tutorials/multi_objective_model_selection.html) | `nixtla-forecast-evaluation` |
| [Rectify Strategy for Multi-Step Forecasts](https://nixtlaverse.nixtla.io/utilsforecast/docs/tutorials/rectify_strategy.html) | `nixtla-forecast-evaluation` |
| [Evaluation](https://nixtlaverse.nixtla.io/utilsforecast/evaluation.html) | `nixtla-forecast-evaluation` |
| [Feature Engineering - UtilsForecast](https://nixtlaverse.nixtla.io/utilsforecast/feature_engineering.html) | `nixtla-exogenous-forecast`, `nixtla-forecast-evaluation` |
| [utilsforecast](https://nixtlaverse.nixtla.io/utilsforecast/index.html) | `nixtla-forecast-evaluation` |
| [Losses](https://nixtlaverse.nixtla.io/utilsforecast/losses.html) | `nixtla-forecast-evaluation` |
| [Plotting](https://nixtlaverse.nixtla.io/utilsforecast/plotting.html) | `nixtla-forecast-evaluation` |
| [Preprocessing](https://nixtlaverse.nixtla.io/utilsforecast/preprocessing.html) | `nixtla-forecast-evaluation`, `nixtla-time-series-data` |

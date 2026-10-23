# Nixtla Skills

A collection of agent skills for forecasting, anomaly detection, and time-series
workflows with TimeGPT and the Nixtlaverse. Skills help coding agents choose the
right data contract, build a working analysis, and validate the result.

## Install

```bash
npx skills add DidierRLopes/nixtla
```

Choose the workflows and agents to install. Install one workflow directly:

```bash
npx skills add DidierRLopes/nixtla --skill nixtla-timegpt-forecast
```

Preview the available collection or install every workflow:

```bash
npx skills add DidierRLopes/nixtla --list
npx skills add DidierRLopes/nixtla --skill '*' --yes
```

Use `--global` to install across projects. The skills CLI supports agents including
Claude Code, Codex, and Cursor; select the agents appropriate to your environment.
Installing a skill supplies instructions and references. Python packages, TimeGPT
credentials, and any cloud environment are configured only when a workflow needs them.

Some supplied documentation describes TimeGPT APIs absent from the `nixtla` 0.7.2
release used in local verification. The recipes identify those requirements and
direct agents to check the installed SDK before using them.

## Choose by the job

| You want to... | Skill |
| --- | --- |
| Fix gaps, timestamps, duplicates, or input layout | [nixtla-time-series-data](skills/nixtla-time-series-data/SKILL.md) |
| Get a fast forecast using the TimeGPT foundation model | [nixtla-timegpt-forecast](skills/nixtla-timegpt-forecast/SKILL.md) |
| Add prices, promotions, weather, holidays, or other drivers | [nixtla-exogenous-forecast](skills/nixtla-exogenous-forecast/SKILL.md) |
| Investigate outliers or monitor recent observations | [nixtla-anomaly-detection](skills/nixtla-anomaly-detection/SKILL.md) |
| Improve and reuse an adapted TimeGPT model | [nixtla-timegpt-finetune](skills/nixtla-timegpt-finetune/SKILL.md) |
| Forecast locally with statistical or intermittent-demand models | [nixtla-statsforecast](skills/nixtla-statsforecast/SKILL.md) |
| Train lag-feature models with sklearn, LightGBM, or XGBoost | [nixtla-mlforecast](skills/nixtla-mlforecast/SKILL.md) |
| Train NHITS, TFT, transformers, or other neural models | [nixtla-neuralforecast](skills/nixtla-neuralforecast/SKILL.md) |
| Make product, store, region, or time totals agree | [nixtla-hierarchical-forecast](skills/nixtla-hierarchical-forecast/SKILL.md) |
| Compare models through realistic historical backtests | [nixtla-forecast-evaluation](skills/nixtla-forecast-evaluation/SKILL.md) |
| Get calibrated intervals, quantiles, or coverage diagnostics | [nixtla-probabilistic-forecast](skills/nixtla-probabilistic-forecast/SKILL.md) |
| Compare plans, explain predictions, or estimate joint risk | [nixtla-scenario-analysis](skills/nixtla-scenario-analysis/SKILL.md) |
| Run a large panel on an existing cluster or use async jobs | [nixtla-forecast-at-scale](skills/nixtla-forecast-at-scale/SKILL.md) |
| Generate panels, augment training, or test known failure modes | [nixtla-synthetic-data](skills/nixtla-synthetic-data/SKILL.md) |

## Ask in terms of the outcome

- "Forecast weekly demand for each store and SKU, and compare it with a seasonal baseline."
- "Would a promotion increase our probability of exceeding warehouse capacity?"
- "Make the regional and product forecasts add up to the company plan."
- "Find unusual sensor readings while keeping the alert burden manageable."
- "Check whether adding weather improves our energy forecasts without future leakage."

An agent can select an installed skill from the request, or you can name the skill
explicitly. Workflows can be combined: a demand forecast might need data preparation,
a model skill, external drivers, and evaluation. Each skill is independently usable
and includes its own recipes and authoritative source catalog.

## Design and sources

The collection is organized by the user's forecasting decisions. Model families
stay separate where their APIs and training contracts differ. Shared analytical
jobs such as backtesting or uncertainty work across the relevant families.

The source material is the [TimeGPT documentation](https://www.nixtla.io/docs/llms-full.txt)
and [Nixtlaverse documentation](https://nixtlaverse.nixtla.io/llms-full.txt).
The [coverage map](docs/source-coverage.md) records source provenance, page routing,
and conflicting or version-sensitive guidance. Recipes are concise adaptations;
the live docs and installed package determine current capabilities.

Use [local verification](docs/validation.md) when editing or trying the collection.

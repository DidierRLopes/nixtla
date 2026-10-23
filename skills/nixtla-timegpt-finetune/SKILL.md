---
name: nixtla-timegpt-finetune
description: Adapt TimeGPT to a dataset and reuse saved fine-tuned models. Use when improving a zero-shot TimeGPT forecast, selecting fine-tuning steps, depth or loss, or managing reusable fine-tuned model IDs.
---

# Nixtla TimeGPT Fine-Tuning

Accept fine-tuning only when it improves the intended forecast on data excluded from adaptation.

## Workflow

1. Establish a zero-shot baseline, deployment, available base model, horizon, frequency, and business metric. Fix chronological training, tuning, and untouched test periods before any fine-tuning.
2. Verify the installed SDK's fine-tuning signature and account model support. Older tutorial model names and defaults can differ from current forecast defaults; record the selected base model explicitly.
3. Use inline `forecast(..., finetune_steps=...)` for a small adaptation experiment or `finetune(...)` when the resulting model must be reused. Read [recipes](references/recipes.md) before choosing the lifecycle.
4. Compare a bounded, declared set of steps, depth, and loss settings against zero-shot performance on identical tuning folds. Fine-tune anew inside each fold or use a model trained strictly before every scored cutoff.
5. Score the selected configuration on the untouched test period. Report per-series and aggregate gains or regressions, runtime, and which experiments actually ran.
6. For reuse, save the returned model ID alongside base model, frequency, feature schema, training cutoff, SDK version, and measured results. Forecast with the matching base model and ID. List or inspect saved model metadata when needed.

## Rules

- A model fine-tuned on the full dataset leaks information into earlier backtest windows even if the forecast input is truncated later.
- Depth ranges from 1 to 5 in the supplied docs. Greater depth and more steps can overfit; do not present them as monotonic accuracy improvements.
- Percentage losses can misbehave around zero demand. Choose a loss suited to the target and evaluate the business metric separately.
- Do not delete saved models merely to tidy experiments unless deletion is part of the user's request.
- The [source catalog](references/sources.md) links the fine-tuning, persistence, SDK, and async lifecycle contracts.

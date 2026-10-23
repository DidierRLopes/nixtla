---
name: nixtla-synthetic-data
description: Generate, augment, and stress-test time-series data with Nixtla SynForecast. Use for reproducible synthetic panels, cold-start experiments, training augmentation, anomaly or missingness injection, and forecasting robustness benchmarks with known ground truth.
---

# Nixtla Synthetic Time Series

Create data with controlled temporal behavior and test its value on untouched real observations when used for learning.

## Workflow

1. Identify whether the task is a reproducible fixture, stress test, training augmentation, or pretraining. Specify frequency, length, series count, target constraints, dependence, and phenomena that must be represented.
2. Verify the installed SynForecast API. Use a domain or statistical generator with interpretable controls when realism matters; use the broad generator pool for diversity rather than pretending it matches a specific business.
3. Generate with explicit seeds and preserve generator provenance. Check schema, finite targets, timestamp regularity, lengths, ID uniqueness, and domain constraints. Preserve intentional anomalies, gaps, and labels separately from ordinary validation failures.
4. For augmentation, split real data first and fit generator selection and parameters on training data only, separately at each evaluation cutoff. Keep observed and synthetic IDs distinguishable and avoid overwriting real rows.
5. Compare observed-only, augmented, and independent-synthetic training under the same real held-out evaluation. For robustness tests, vary one corruption mechanism at a time and score against known uncorrupted targets or event labels.
6. Deliver the generation recipe, seed and parameter manifest, provenance or event labels, validation report, and the measured value or limitation of synthetic data.

## Rules

- Anomaly ground-truth labels are evaluation artifacts, not future-known model features in a real deployment.
- Augmenting before a chronological split leaks information. Similar-looking synthetic examples are not independent evidence of predictive accuracy.
- Synthetic data fitted to private histories is not automatically anonymized or safe to share. Independent generation and fitted augmentation have different provenance.
- The source describes SynForecast as alpha. Verify installed generator parameters and engine output types rather than copying a newer example into an older release.
- Read [recipes](references/recipes.md) for generation, augmentation and robustness patterns; use [sources](references/sources.md) for specialized generators, exogenous variables, and integrations.

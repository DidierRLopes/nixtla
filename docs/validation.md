# Local verification

Skills are instructions, so validation needs both installability and realistic
use. Metadata checks alone cannot establish that an agent builds a valid forecast.

## Discover and install

From the repository root, list the collection without installing it:

```bash
DISABLE_TELEMETRY=1 npx --yes skills add . --list
```

To test installation without changing your current project's agent configuration:

```bash
repo_dir="$PWD"
trial_dir="$(mktemp -d)"
cd "$trial_dir"
DISABLE_TELEMETRY=1 npx --yes skills add "$repo_dir" --skill '*' --agent codex --yes --copy
```

Inspect `.agents/skills` in that temporary project. Every installed skill should
retain its entrypoint, recipes, source catalog, and agent metadata. Test other
target agents through the skills CLI's agent selector when they are relevant.
The GitHub shorthand uses the files published to the repository's default branch;
a successful local install does not publish uncommitted changes.

## Exercise the workflows

Use a temporary Python environment and install only the libraries for the selected
recipe. Construct a small panel with known seasonality, multiple IDs, and a held-out
future. Read each skill and its recipe as an agent would, then execute the workflow
through the library's public API. Check predictions and decisions, not whether the
agent repeated the skill's wording.

Useful acceptance cases:

- A transactional sales source with duplicate ID/date pairs and absent days. Resolve duplicates by source meaning, preserve observed zeros, and record the policy for missing dates.
- Identical rolling origins for a seasonal baseline, statistical model, and lag-feature model, with and without a future-known driver. Account for every expected scoring key and report regressions as well as improvements.
- Neural fitting followed by save, reload, and prediction from the same eligible history. Compare actual forecast values after aligning keys.
- Regional and store forecasts reconciled through BottomUp and nonnegative MinTrace. Verify numerical sums and nonnegativity at every future timestamp.
- Conformal calibration on earlier windows, followed by interval scoring on later observations. Inspect effective samples and coverage without assuming nominal coverage is achieved.
- Seeded synthetic generation and training-only augmentation. Verify repeated draws, original-row preservation, synthetic ID handling, and exclusion of real validation rows.
- Credential-free inspection of TimeGPT signatures. Generate only calls supported by the installed SDK; identify unavailable methods without inventing results.

For new or changed workflows, use a fresh agent with a realistic request and only
the skill's normal references. Keep trial artifacts outside the repository and
review the resulting code, outputs, and unexecuted branches.

## Verification record: 2026-10-23

All 14 entrypoints passed the skill-creator metadata validator. Agent metadata,
relative Markdown links, and Python recipe syntax were also checked. The skills
CLI discovered and copied all 14 skills into an isolated Codex project, including
their supporting references.

Three fresh-agent trials exercised the acceptance cases above. Statistical,
machine-learning, data-preparation, exogenous-feature, and evaluation workflows
completed across a two-SKU daily panel and three 14-day rolling windows. The
planned-price feature improved RMSE but worsened MAE in that synthetic example;
the trial did not claim a universal improvement.

The exact Python snippets in the data-preparation, StatsForecast, MLForecast,
NeuralForecast, hierarchy, conformal, and synthetic recipes were also executed
with suitable local input variables. Checks covered inserted gaps, complete
future grids, finite forecasts, identical reloaded neural predictions, coherent
reconciliation columns, valid interval bounds, and augmented series identities.
Dependency output included PyTorch Lightning deprecation notices and a solver's
sparse-matrix conversion notices; these did not fail execution and were not
suppressed.

Neural save/reload produced identical predictions. Both tested reconciliation
methods had zero measured parent-versus-child sum discrepancy, and their outputs
were nonnegative. Split conformal returned the documented interval axes and
covered 11 of 14 later observations for a 90% target. That small holdout checks the
workflow and exposes its measured coverage; it does not establish long-run
calibration. Seeded synthetic panels reproduced exactly, and augmentation used
training rows only.

The temporary environment used Python 3.12.11, StatsForecast 2.0.1, MLForecast
1.0.2, NeuralForecast 3.3.0, HierarchicalForecast 1.5.3, ConformalForecast 0.1.0,
SynForecast 0.2.0, Nixtla 0.7.2, and UtilsForecast 0.2.17. These are the versions
observed during verification, not imposed runtime pins.

No paid TimeGPT requests, Azure deployments, distributed clusters, or hosted
serving endpoints were executed. The installed TimeGPT package lacks several
methods present in the supplied documentation; affected recipes identify that
boundary. Public GitHub installation and skills.sh listing require publishing
the files and are separate from the completed local checks.

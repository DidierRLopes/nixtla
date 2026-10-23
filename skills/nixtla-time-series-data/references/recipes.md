# Data preparation recipes

## Normalize a panel

Install only the packages needed for this workflow: `pandas` and `utilsforecast`.
Here `raw` is a pandas frame; replace the source column names with the user's schema.

```python
import pandas as pd
from utilsforecast.preprocessing import fill_gaps

panel = raw.rename(columns={"sku": "unique_id", "date": "ds", "sales": "y"}).copy()
panel["ds"] = pd.to_datetime(panel["ds"], errors="raise")
panel["y"] = pd.to_numeric(panel["y"], errors="raise")
if panel[["unique_id", "ds"]].isna().any().any():
    raise ValueError("Series IDs and timestamps must be present")
if panel.duplicated(["unique_id", "ds"]).any():
    raise ValueError("Resolve duplicate series/timestamp keys before forecasting")
panel = panel.sort_values(["unique_id", "ds"]).reset_index(drop=True)
# This inserts missing timestamps; it does not impute y.
panel = fill_gaps(panel, freq="D", start="per_serie", end="per_serie")
```

Do not fill `y` until the missingness policy is decided. For wide data, melt only the target series columns; retain identifiers and timestamps. A single series can use a constant ID. Normalize timezone handling consistently and retain the original timestamps when converting.

## Audit with the TimeGPT client

When the installed `nixtla` SDK exposes `audit_data`, it returns
`all_pass, fail_dfs, case_specific_dfs`. `clean_data` consumes the audit dictionaries
and returns a new frame plus updated audit outputs. Check signatures in the installed
SDK before using these methods. Keep `clean_case_specific=False` unless the user has
established that negative values or leading zeros are errors. Re-audit after cleaning;
cleaning can create new gaps or missing target values.

## Frequency decisions

- Calendar frequency describes timestamp spacing; `season_length` is the number of observations in a recurring pattern. Daily data can have weekly seasonality of seven.
- `MS` is month start. Month-end aliases and Polars duration strings can differ from pandas aliases; use the installed backend's supported offset.
- Use a custom business calendar for market sessions. Do not insert weekends just to make a financial series daily.
- For integer time indices use the supported integer step. Preserve a mapping to original dates if you regularize to integer steps.
- Different series can start at different times. Do not create artificial pre-launch history to equalize their lengths.

Read the source catalog's missing-values and irregular-timestamps guides before handling those cases. The snapshot's quickstart rejects target NaNs while its missing-values tutorial allows them; test the selected model and SDK instead of treating either statement as universal.

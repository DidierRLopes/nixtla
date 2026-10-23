# Hierarchy recipes

Install `hierarchicalforecast`, `statsforecast`, and the selected frame backend.
`bottom` has `region`, `store`, `ds`, and `y`, with one row per bottom entity/time.
The example assumes store codes are unique within a region.

```python
from hierarchicalforecast.utils import aggregate
from hierarchicalforecast.core import HierarchicalReconciliation
from hierarchicalforecast.methods import BottomUp, MinTrace
from statsforecast import StatsForecast
from statsforecast.models import AutoETS

spec = [["region"], ["region", "store"]]
Y_df, S_df, tags = aggregate(df=bottom, spec=spec)
sf = StatsForecast(models=[AutoETS(season_length=7)], freq="D", n_jobs=1)
base = sf.forecast(df=Y_df, h=14)
hrec = HierarchicalReconciliation(
    reconcilers=[BottomUp(), MinTrace(method="ols", nonnegative=True)]
)
reconciled = hrec.reconcile(Y_hat_df=base, Y_df=Y_df, S_df=S_df, tags=tags)
```

This spec has region totals and region/store leaves. Add a documented top level
only if needed; do not label the example as including a company-wide total.
Keep actual ID labels from `aggregate`, rather than manually reconstructing them
with separators that may collide with entity values.

## Residuals and IDs

If the selected method estimates error covariance, retain base-model fitted values
and join them to observed history by ID/time. They need to correspond to the same
models whose future columns are reconciled. Align matrix rows and bottom columns
explicitly; do not assume DataFrame sort order matches the summing matrix.
DataFrame index versus ID-column conventions vary across older examples. Inspect
the installed `reconcile` contract before adding `reset_index` indiscriminately.

## Coherence and uncertainty

The returned frame can retain the original, incoherent base-model columns beside
new model/method reconciliation columns. Identify those sets explicitly; verify
and label reconciled columns as coherent rather than applying that claim to the
entire returned frame.

For each reconciled forecast column and timestamp, take the bottom-level vector
`b`, compute `S @ b`, and compare it to all-level predictions in the matrix's row
order. Also check required nonnegativity. Built-in diagnostics can supplement this
check when the installed version provides them.

Normality, bootstrap, and PERMBU are distinct uncertainty methods. Select one from
the residual and dependence assumptions, evaluate coverage by level, and use
reconciled samples for aggregate risk. The sum of per-series 95th percentiles is
not generally the 95th percentile of the total.

For large structures, the latest docs support `aggregate(..., sparse_s=True)`
returning an `SMatrix`; older releases may return a different sparse interface.
Use the installed version's sparse reconciliation contract. Temporal, THIEF, and
cross-temporal examples need their own temporal alignment and level definitions.

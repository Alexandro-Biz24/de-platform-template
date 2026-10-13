# Bronze layer costs

- **Pricing date:** 2026-10-12
- **Region:** `europe-west1`
- **Storage class:** Standard
- **Pricing source:** [Google Cloud Storage pricing](https://cloud.google.com/storage/pricing)
- **Standard storage:** `$0.020/GiB-month`
- **Class A operations:** `$0.005/1,000 operations`

## Final Bronze volume

| Metric | Value |
|---|---:|
| Tables | `{{TABLE_COUNT}}` |
| Parquet objects | `{{TOTAL_OBJECTS}}` |
| Total bytes | `{{TOTAL_BYTES}}` |
| Total GiB | `{{TOTAL_GIB}}` |

## Monthly cost

### Storage

$$
\text{Storage cost}
=
\frac{\text{total bytes}}{1024^3}
\times 0.020
$$

$$
\text{Storage cost}
=
\frac{\text{ {{TOTAL_BYTES}} }}{1024^3}
\times 0.020
=
\text{ {{STORAGE_COST_USD}} USD/month}
$$

### Class A operations

One Parquet object creation is counted as one Class A operation.

$$
\text{Class A cost}
=
\frac{\text{object count}}{1000}
\times 0.005
$$

$$
\text{Class A cost}
=
\frac{\text{ {{TOTAL_OBJECTS}} }}{1000}
\times 0.005
=
\text{ {{CLASS_A_COST_USD}} USD}
$$

This estimate assumes one complete Bronze ingestion per month. Otherwise, the Class A cost is a one-time ingestion cost.

## Cost summary

| Component | Monthly cost |
|---|---:|
| Standard storage | `{{STORAGE_COST_USD}} USD` |
| Class A object creation | `{{CLASS_A_COST_USD}} USD` |
| **Estimated total** | **`{{TOTAL_COST_USD}} USD/month`** |

BigQuery query costs are not included because the monthly query frequency is not yet known. The audit records `query_bytes_processed` so this cost can be estimated later.

## One-hundred-times-larger scenario

If the data volume became 100 times larger while keeping the same layout and ingestion frequency, storage cost would increase approximately 100 times. The number of objects and Class A operation cost could also approach 100 times their current values unless the pipeline writes larger Parquet files.

Estimated cost at 100 times the current scale:

$$
\text{ {{TOTAL_COST_USD}} } \times 100
=
\text{ {{TOTAL_COST_100X_USD}} USD/month}
$$

This projection excludes network transfer, BigQuery queries and lifecycle-transition operations.
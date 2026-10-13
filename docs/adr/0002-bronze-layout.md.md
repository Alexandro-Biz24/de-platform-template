# ADR-0000: Title stated as the decision

*Example title: "Store raw data as Parquet files in Cloud Storage".*

- **Status:** proposed | accepted | superseded by ADR-XXXX
- **Date:** YYYY-MM-DD
- **Author:**
- **Lesson:** L0X

## Context

Albert’s Marketplace provides 27 legacy CSV tables containing transactional, reference and personal data. The source inventory produced by the ingestion notebook shows that `cart`, `cart_items` and `returns` are empty, while some reference tables contain only a few rows. Other tables contain tens or hundreds of thousands of rows.

The Bronze layer must preserve the received data without cleaning, deduplication or dropped columns. The files must be stored in the group Cloud Storage bucket in `europe-west1` and remain queryable through BigQuery external tables.

The audit configuration in `explore_data_mapping.json` layouts:  unpartitioned Parquet references and partitioned alternatives. They are compared using object count, stored bytes, storage cost, Class A operation cost, BigQuery execution time and bytes processed. The limited size of the provided samples means that query-time differences must be interpreted together with expected production workloads and the risk of creating small files.

## Options considered


| Option | For | Against |
|---|---|---|
| Original CSV for all tables | Preserves the delivery format and is easy to inspect | Larger files, weaker type preservation, no columnar reading and no partition pruning |
| Unpartitioned Snappy Parquet for all 27 tables | Compressed, typed, simple to manage and suitable for small, empty or reference tables | Queries may scan the complete table |
| Date-partitioned Parquet for `daily_deals`, `orders`, `shipment` and `subscription` | Supports common time-range filters and chronological processing | Daily cardinality may create many small files |
| Category-partitioned Parquet for `payment`, `product`, `review`, `seller`, `shipment` and `shipping_details` | Supports common filters such as method, category, rating, seller type, carrier and country | Ineffective when filters do not use the selected key; partitions may be unbalanced |
| Multi-column Parquet for `review` and `shipping_details` | Can improve filtering by seller-product flag and rating, or by country and state | Creates more objects and increases the risk of small files and higher write-operation costs |

## Criteria

The layouts were evaluated using four quantitative audit metrics:

1. **Monthly storage cost:** the estimated monthly cost of storing each layout in Cloud Storage.
2. **Object creation cost:** the Class A operation cost generated when creating the Parquet objects.
3. **Query execution time:** the elapsed time of the representative BigQuery `SELECT`.
4. **Bytes processed:** the amount of data processed by BigQuery for the same query.

A partition key was considered relevant when it also satisfied four design criteria:

5. **Frequent filtering:** the column is commonly used in `WHERE` clauses.
6. **Stable values:** the partition value is unlikely to change after ingestion.
7. **Controlled cardinality:** the key does not create an excessive number of partitions.
8. **Balanced partition size:** partitions contain enough rows and remain reasonably balanced.

## Decision

What you chose, in one or two sentences.

## Consequences

What becomes easier, what becomes harder, and what you will have to watch.

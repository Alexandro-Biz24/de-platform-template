# ADR-0001: Title stated as the decision

*Example title: "Store raw data as Parquet files in Cloud Storage".*

- **Status:** proposed 
- **Date:** 2026-10-09
- **Author:** Alexandro
- **Lesson:** L01

## Context

Albert's Marketplace currently uses one PostgreSQL database containing 25 tables
for both the customer-facing shop and analytical workloads. All data seems to be structured. 

Analysts query the production database directly and also use nightly CSV exports
in spreadsheets. This creates workload contention, manual processes and two
different paths for computing metrics. 

The database also contains sensitive saved-card and password data, which should
not be exposed to the analytical platform.

The ML team needs a reliable table containing units sold per product, per country and per day. 

## Options considered

| Option | For | Against |
| Cloud data warehouse | Strong SQL performance, familiar to analysts, clear governance, structured dimensional models, low operational complexity | Less suitable for storing large volumes of unstructured files |
| Data lake | Cheap and flexible storage for any data type, preserves raw data | Requires an external compute engine, no ACID garanties, less convenient for spreadsheet and SQL users |
| Two-tier architecture | Combines flexible raw storage in a lake with performant analytics in a warehouse | Creates two systems, duplicated data and additional pipelines to maintain |
| Lakehouse | Supports BI, SQL and ML on shared storage with ACID transactions and medallion layers | More complex to configure and operate than required for the current structured-data use case |

## Criteria

Scoring: 1 = poor, 2 = acceptable, 3 = strong.

| Criterion | Warehouse | Lake | Two-tier | Lakehouse |
|---|---:|---:|---:|---:|
| Structured analytical workload | 3 | 1 | 3 | 3 |
| SQL accessibility for analysts | 3 | 1 | 3 | 2 |
| ML-ready structured tables | 3 | 2 | 3 | 3 |
| Governance and metric consistency | 3 | 1 | 3 | 3 |
| Team skills and operational simplicity | 3 | 1 | 1 | 2 |
| Cost for the current scope | 3 | 3 | 1 | 2 |
| Support for unstructured data | 1 | 3 | 3 | 3 |
| **Total** | **19** | **12** | **17** | **18** |

The warehouse scores highest because the current sources and required outputs are mainly structured

## Decision

We will use a cloud data warehouse as the target analytical platform.
Data will be organised into Bronze, Silver and Gold layers inside the warehouse

## Consequences

What becomes easier, what becomes harder, and what you will have to watch.

Analytical queries will no longer compete with the customer-facing PostgreSQL
database + sharing methodologie 

Need to build and monitor ingestion and transformation pipeline
Warehouse query and storage costs must also be monitored.

If the marketplace later needs to store unstructured data the architecture no longer fit
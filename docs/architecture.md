# Architecture

> Update this page at the end of every lesson. It is the diagram you present at
> the oral defence.

## Context

## Context

Albert's Marketplace needs to separate analytical workloads from the operational
PostgreSQL database used by the customer-facing website. Analysts need governed
and consistent metrics instead of direct SQL queries and manually processed CSV
exports. The ML team needs reliable daily sales data by product and country.
Sensitive saved-card and password data must never enter the analytical platform.

Lesson 2 implements the first part of this architecture: a Bronze layer stored as
Snappy-compressed Parquet files in a group Cloud Storage bucket located in
`europe-west1`.

## Target architecture

```mermaid
flowchart LR
    A["Customers and sellers"] --> B["Web shop"]
    B <--> C["Operational PostgreSQL"]
    C --> D["Legacy CSV exports"]
    D --> E["Python ingestion notebook"]

    S["Passwords and saved-card data"] -. "Excluded" .-> E

    subgraph BRONZE["Bronze layer — Cloud Storage — europe-west1"]
        direction TB

        F["Group bucket<br/>GROUP_BUCKET_NAME"]
        G["bronze/table/"]
        H["Snappy Parquet files<br/>Table-specific partitioning"]
        U["Authorised project members<br/>Read access to the entire Bronze layer"]

        F --> G --> H
        U -. "IAM access" .-> F
    end

    E --> F
```



## Layers

| Layer | What lands there | Transformations | Guarantee |
|---|---|---|---|
| Bronze | Source-aligned copies of orders, customers, products and reviews | Minimal validation and ingestion metadata added; passwords and saved-card data excluded | Authorised source data is preserved and traceable |
| Silver | Cleaned orders, customers, products and reviews | Deduplication, type validation, standardised dates and countries, joins and shared revenue rules | One clean and governed version of each business fact |
| Gold | Reporting data marts, dimensions, fact tables and ML-ready datasets | Business aggregations and dimensional modelling | Data is ready for a defined analytical or ML use case |
  
## Decisions

| ADR | Decision | Status |
|---|---|---|
| [0001](adr/0001-target-architecture.md) | Use a cloud data warehouse as the target analytical platform | Accepted |
| [0002](adr/0002-bronze-layout.md) | Store Bronze data as Snappy-compressed Parquet with table-specific layouts | Proposed |

## Change log

| Lesson | What changed |
|---|---|
| L01 | Defined the target architecture and separation between operational and analytical workloads |
| L02 | Added the group Bronze bucket, Parquet ingestion, layout audit, BigQuery external validation, lifecycle policy and planned IAM policy |

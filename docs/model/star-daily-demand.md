## Business process

The business process being measured is daily product sales and demand across
countries.

## Grain

One row in `fct_daily_demand` represents the total units sold for one product,
in one delivery country, on one calendar day.

## Dimensions

### `dim_product`

| Column | Description |
|---|---|
| `product_key` | Warehouse surrogate key |
| `product_id` | Product identifier from the source system |
| `product_name` | Product name |
| `category` | Product category |

### `dim_country`

| Column | Description |
|---|---|
| `country_key` | Warehouse surrogate key |
| `country_code` | ISO country code |
| `country_name` | Country name |
| `region` | Geographical region |

### `dim_date`

| Column | Description |
|---|---|
| `date_key` | Date key in `YYYYMMDD` format |
| `full_date` | Calendar date |
| `day_of_week` | Day of the week |
| `month` | Calendar month |
| `quarter` | Calendar quarter |
| `year` | Calendar year |

## Facts

### `fct_daily_demand`

| Column | Type | Description |
|---|---|---|
| `date_key` | Foreign key | References `dim_date` |
| `product_key` | Foreign key | References `dim_product` |
| `country_key` | Foreign key | References `dim_country` |
| `units_sold` | Additive fact | Total quantity of units sold |

## Schema

```mermaid
erDiagram
    DIM_DATE ||--o{ FCT_DAILY_DEMAND : describes
    DIM_PRODUCT ||--o{ FCT_DAILY_DEMAND : describes
    DIM_COUNTRY ||--o{ FCT_DAILY_DEMAND : describes

    FCT_DAILY_DEMAND {
        int date_key FK
        int product_key FK
        int country_key FK
        int units_sold
    }

    DIM_DATE {
        int date_key PK
        date full_date
        string day_of_week
        int month
        int quarter
        int year
    }

    DIM_PRODUCT {
        int product_key PK
        string product_id
        string product_name
        string category
    }

    DIM_COUNTRY {
        int country_key PK
        string country_code
        string country_name
        string region
    }
```

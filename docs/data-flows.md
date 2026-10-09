# Data flows

One row per flow: where the data comes from, what it is, who uses it, how often
it moves, and in which format.

| # | Source | Data | Consumer | Frequency | Format |
|---|---|---|---|---|---|
| 1 | Website | Orders, customer information, reviews, saved cards and passwords | PostgreSQL | Real time | Structured SQL records |
| 2 | PostgreSQL | Products, customer accounts and order information | Website | On demand | SQL query results |
| 3 | PostgreSQL | Orders, customers, products and reviews | Analysts | On demand | Direct SQL queries |
| 4 | PostgreSQL | Reporting data | CSV export process | Nightly | CSV |
| 5 | CSV exports | Reporting data | Analysts using spreadsheets | After each nightly export | CSV imported into spreadsheets |

## Under the matrix, answer

- Which flows carry personal data?
Flows 1, 2 and 3 may carry personal data because they contain customer
or order information. Flow 1 also carries highly sensitive saved-card and
password data.

- Which consumers read directly from a system that also serves customers?

The website, analysts and the CSV export process read directly from PostgreSQL.
Analysts are the problematic consumer because they query the production database
that also serves the website's customers

- Where could the same figure be computed twice, in two different ways?
Revenue could be calculated once by analysts through direct SQL queries and
again in spreadsheets using the nightly CSV exports. Different filters,
deduplication rules or definitions of revenue could produce different results
---
editable: false
---

# RANK_DENSE (window)



#### Syntax {#syntax}

{% list tabs %}

- Standard

  ```
  RANK_DENSE( value [ , direction ] )
  ```

- Extended

  ```
  RANK_DENSE( value [ , direction ]
              [ TOTAL | WITHIN ... | AMONG ... ]
              [ BEFORE FILTER BY ... ]
            )
  ```

  More info:
  - [TOTAL, WITHIN, AMONG](window-functions.md#syntax-grouping)
  - [BEFORE FILTER BY](window-functions.md#syntax-before-filter-by)

{% endlist %}

#### Description {#description}
Returns the rank of the current row if ordered by the given argument. Rows corresponding to the same value used for sorting have the same rank. If the first two rows both have rank of `1`, then the next row (if it features a different value) will have rank `2`, (rank without gaps).

If `direction` is `"desc"` or omitted, then ranking is done from greatest to least, if `"asc"`, then from least to greatest.

See also [RANK](RANK.md), [RANK_UNIQUE](RANK_UNIQUE.md), [RANK_PERCENTILE](RANK_PERCENTILE.md).

**Argument types:**
- `value` — `Boolean | Date | Datetime | Fractional number | Integer | String | UUID`
- `direction` — `String`


**Return type**: `Integer`

{% note info %}

Only constant values are accepted for the arguments (`direction`).

{% endnote %}


#### Examples {#examples}

{% cut "Example with two arguments" %}


Source data

| **Date**       | **City**          | **Category**        | **Orders**   | **Profit**   |
|:---------------|:------------------|:--------------------|:-------------|:-------------|
| `'2019-03-01'` | `'London'`        | `'Office Supplies'` | `8`          | `120.80`     |
| `'2019-03-04'` | `'London'`        | `'Office Supplies'` | `2`          | `100.00`     |
| `'2019-03-05'` | `'London'`        | `'Furniture'`       | `1`          | `750.00`     |
| `'2019-03-02'` | `'Moscow'`        | `'Furniture'`       | `2`          | `1250.50`    |
| `'2019-03-03'` | `'Moscow'`        | `'Office Supplies'` | `4`          | `85.00`      |
| `'2019-03-01'` | `'San Francisco'` | `'Office Supplies'` | `23`         | `723.00`     |
| `'2019-03-01'` | `'San Francisco'` | `'Furniture'`       | `1`          | `1000.00`    |
| `'2019-03-03'` | `'San Francisco'` | `'Furniture'`       | `4`          | `4000.00`    |
| `'2019-03-02'` | `'Detroit'`       | `'Furniture'`       | `5`          | `3700.00`    |
| `'2019-03-04'` | `'Detroit'`       | `'Office Supplies'` | `25`         | `1200.00`    |
| `'2019-03-04'` | `'Detroit'`       | `'Furniture'`       | `2`          | `3500.00`    |

Grouped by `[City]`.

Sorted by `[City]`.

Result

| **[City]**        | **SUM([Orders])**   | **RANK_DENSE(SUM([Orders]), "desc")**   | **RANK_DENSE(SUM([Orders]), "asc")**   |
|:------------------|:--------------------|:----------------------------------------|:---------------------------------------|
| `'Detroit'`       | `32`                | `1`                                     | `4`                                    |
| `'London'`        | `11`                | `3`                                     | `2`                                    |
| `'Moscow'`        | `6`                 | `4`                                     | `1`                                    |
| `'San Francisco'` | `28`                | `2`                                     | `3`                                    |

{% endcut %}

{% cut "Example with grouping" %}


Source data

| **Date**       | **City**          | **Category**        | **Orders**   | **Profit**   |
|:---------------|:------------------|:--------------------|:-------------|:-------------|
| `'2019-03-01'` | `'London'`        | `'Office Supplies'` | `8`          | `120.80`     |
| `'2019-03-04'` | `'London'`        | `'Office Supplies'` | `2`          | `100.00`     |
| `'2019-03-05'` | `'London'`        | `'Furniture'`       | `1`          | `750.00`     |
| `'2019-03-02'` | `'Moscow'`        | `'Furniture'`       | `2`          | `1250.50`    |
| `'2019-03-03'` | `'Moscow'`        | `'Office Supplies'` | `4`          | `85.00`      |
| `'2019-03-01'` | `'San Francisco'` | `'Office Supplies'` | `23`         | `723.00`     |
| `'2019-03-01'` | `'San Francisco'` | `'Furniture'`       | `1`          | `1000.00`    |
| `'2019-03-03'` | `'San Francisco'` | `'Furniture'`       | `4`          | `4000.00`    |
| `'2019-03-02'` | `'Detroit'`       | `'Furniture'`       | `5`          | `3700.00`    |
| `'2019-03-04'` | `'Detroit'`       | `'Office Supplies'` | `25`         | `1200.00`    |
| `'2019-03-04'` | `'Detroit'`       | `'Furniture'`       | `2`          | `3500.00`    |

Grouped by `[City]`, `[Category]`.

Sorted by `[City]`, `[Category]`.

Result

| **[City]**        | **[Category]**      | **SUM([Orders])**   | **RANK_DENSE(SUM([Orders]) TOTAL)**   | **RANK_DENSE(SUM([Orders]) WITHIN [City])**   | **RANK_DENSE(SUM([Orders]) AMONG [City])**   |
|:------------------|:--------------------|:--------------------|:--------------------------------------|:----------------------------------------------|:---------------------------------------------|
| `'Detroit'`       | `'Furniture'`       | `7`                 | `4`                                   | `2`                                           | `1`                                          |
| `'Detroit'`       | `'Office Supplies'` | `25`                | `1`                                   | `1`                                           | `1`                                          |
| `'London'`        | `'Furniture'`       | `1`                 | `8`                                   | `2`                                           | `4`                                          |
| `'London'`        | `'Office Supplies'` | `10`                | `3`                                   | `1`                                           | `3`                                          |
| `'Moscow'`        | `'Furniture'`       | `2`                 | `7`                                   | `2`                                           | `3`                                          |
| `'Moscow'`        | `'Office Supplies'` | `4`                 | `6`                                   | `1`                                           | `4`                                          |
| `'San Francisco'` | `'Furniture'`       | `5`                 | `5`                                   | `2`                                           | `2`                                          |
| `'San Francisco'` | `'Office Supplies'` | `23`                | `2`                                   | `1`                                           | `2`                                          |

{% endcut %}


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 19.13`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`.

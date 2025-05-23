---
editable: false
---

# MEDIAN



#### Syntax {#syntax}

{% list tabs %}

- Standard

  ```
  MEDIAN( value )
  ```

- Extended

  ```
  MEDIAN( value
          [ FIXED ... | INCLUDE ... | EXCLUDE ... ]
          [ BEFORE FILTER BY ... ]
        )
  ```

  More info:
  - [FIXED, INCLUDE, EXCLUDE](aggregation-functions.md#syntax-lod)
  - [BEFORE FILTER BY](aggregation-functions.md#syntax-before-filter-by)

{% endlist %}

#### Description {#description}
Returns the median value.

**Argument types:**
- `value` — `Date | Datetime | Fractional number | Integer`


**Return type**: Same type as (`value`)

#### Example {#examples}

```
MEDIAN([Profit])
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 19.13`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.4`, `YDB`.

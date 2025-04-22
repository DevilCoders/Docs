### Так можно сделать запрос в Greenplum:
        
```python
import pandas
from connection.greenplum import connection

rows = connection.query("""
SELECT country,
       application_locale,
       COUNT(*) AS cnt
  FROM summary.dm_order
 WHERE moscow_order_dttm > now() - '1 day'::interval
 GROUP BY country, application_locale
 ORDER BY country ASC, cnt DESC;""")

pandas.DataFrame.from_records(
    rows,
    columns=('Страна', 'Локаль', 'Количество'))
```

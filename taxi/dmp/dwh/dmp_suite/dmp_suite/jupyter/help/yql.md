### Так можно сделать YQL запрос:
        
```python
from dmp_suite.yql.operation import YqlSelect

query = YqlSelect("""
   SELECT country,
          application_locale,
          COUNT(*) as cnt
    FROM `home/taxi-dwh/summary/dm_order/2020-05`
    GROUP BY country, application_locale
    ORDER BY country ASC, cnt DESC""")

# Это вернёт pandas DataFrame
query.get_data()
```

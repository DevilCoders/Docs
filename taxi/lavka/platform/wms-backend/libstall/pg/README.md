## Коннектор к БД

Коннектор к одному шарду:

```python

from stall import pg


db = pg.PgShard(dsn)

async with db(mode='slave') as conn:
    rows = conn.fetch(sqlt, {'variable': 123})

```

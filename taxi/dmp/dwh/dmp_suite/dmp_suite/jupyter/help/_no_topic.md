### Помощь по Taxi DMP

Команда `%help` может выдавать справку по таким разделам:

{available_topics}

Попробуй например: `%help yql`

#### Другие способы получения информации

Чтобы посмотреть документацию по табличке, проимпортируй её и введи класс таблицы на отдельной строке.
Например так:

```python
from atlas_etl.layer.clickhouse.ods_order.table import AtlasOdsOrder
AtlasOdsOrder
```

Чтобы посмотреть небольшое количество данных из таблицы, используй команду `%preview <имя таблицы>`

```python
from taxi_etl.layer.yt.ods.mdb.order.table import OdsOrder
%preview OdsOrder
```

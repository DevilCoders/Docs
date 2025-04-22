# Генарация OLAP-кубов на основе регулярных координат и интересов пользователя.

Для корректой отработки шага 3 ожидается, что YQL токен будет выставлен в переменной окружения `YQL_TOKEN`

### Запустить все сразу
Операция совмещает все последующие операции и возвращает таблицу с полигонами и таблицу с OLAP-кубом.

- `in-geo-log-table` - таблица с регулярными координатами. Ожидаем колонки `yuid`, `lat`, `lon`.
- `out-polygon-table` - куда сохранить таблицу с полигонами.
- `out-olap-table` - куда сохранить таблицу с olap-кубом

```
./olap run-all \
    --in-geo-log-table //home/x-products/production/datacloud/grep/geo_log/2020-02-22 \
    --out-polygon-base-table //projects/scoring/tmp/geo/sample/polygon-base \
    --out-olap-table //projects/scoring/tmp/geo/sample/olap
```

Дальше каждый шаг разобран по отдельности.

### 1. Конвертация тоблицы с соцдемом с yandexuid на yuid
Берем у Крипты таблицу сосцдемом (`//home/crypta/production/profiles/export/profiles_for_14days`) и конвертируем yandexuid в yuid.
```
./olap yuid-to-socdem --output-table //projects/scoring/tmp/geo/sample/yuid-to-socdem
```

### 2. Координаты в геохеши (h3, resolution=9)
Конвертируем таблицу с регулярными координатами `geo-log-table`. Переводим lat, lon коорнидаты в геохеш. 

Ожидаемая структура таблице `geo-log-table`:
```
yuid  String (sorted by)
lat   Double
lon   Double
```

Таблица на выходе
```
yuid   String (sorted by)
geo_id String
```

```
./olap latlon-to-geo-id \
    --geo-log-table //home/x-products/production/datacloud/grep/geo_log/2020-02-22 \
    --output-table //projects/scoring/tmp/geo/sample/yuid-to-geo-id
```

### 3. База полигонов
Строим базу полигонов.

- `geo-id-table` - таблица содержащая все необходимые `geo_id`.
- `output-table` - куда сохранять таблицу с полигонами

```
./olap build-polygon-base \
    --geo-id-table //projects/scoring/tmp/geo/sample/yuid-to-geo-id \
    --output-table //projects/scoring/tmp/geo/sample/polygon-base
```

### 4. OLAP
Строим OLAP куб в разрезе по соцдему. Словарь с интересами для OLAP-куба лежит в `data.py`.

- `yuid-to-socdem-table` - таблица с соцдемом из пункта 1.
- `yuid-to-geo-id-table` - таблица с шеохешами их пункта 2.
- `polygon-base-table` - база полигонов полученная в шаге 3.
- `output-table` - куда сохранять результат

```
./olap build-olap \
    --yuid-to-socdem-table //projects/scoring/tmp/geo/sample/yuid-to-socdem \
    --yuid-to-geo-id-table //projects/scoring/tmp/geo/sample/yuid-to-geo-id \
    --output-table //projects/scoring/geo/sample/olap \
    --polygon-base-table //projects/scoring/tmp/geo/sample/polygon-base
```

### Выгрузить таблиц в формате готовом для загрузки в ClickHouse
Выгрузить базу полигонов
```
./olap download-polygons \
    --table //projects/scoring/tmp/geo/sample/polygon-base \
    --local-file polygons.csv
```

Выгрузить OLAP
```
./olap download-olap \
    --olap-table //projects/scoring/tmp/geo/sample/olap \
    --local-file olap.csv
```

### ClickHouse
Подключиться к CH
```
clickhouse-client --host vla-1zwdkyy37cy8iz7f.db.yandex.net --secure --user geo_user --database geo --port 9440 --password
```

Как создана OLAP таблица
```
CREATE TABLE geo.olap_cities (`polygon_id` UInt64, `age` UInt64, `sex` String, `incomelevel` String, `city_id` UInt64, `hash_9` UInt64, `socdem_counts` UInt64, `interest_id` UInt64, `interest_counts` UInt64, `interest_name` String) ENGINE = ReplicatedMergeTree('/clickhouse/tables/shard1/geo_olap_cities', 'vla-1zwdkyy37cy8iz7f.db.yandex.net') ORDER BY (polygon_id, age, sex, incomelevel) SETTINGS index_granularity = 8192
```

Как загружены данные в OLAP таблицу.

`./olap download-olap` выгружает данные из YT в необходимом для загрузки в CH виде. В файле не должно быть хедера, порядок колонок должен совпадать с порядком в CH таблице.

```
clickhouse-client --host vla-1zwdkyy37cy8iz7f.db.yandex.net --secure --user geo_user --database geo --port 9440 --password HERE-SHOULD-BE-PASSWORD --query "INSERT INTO geo.olap_cities FORMAT CSV" --max_insert_block_size=100000 < olap.csv
```

Как создана таблицу с полигонами
```
CREATE TABLE geo.polygons (`lat` Double, `lon` Double, `country_id` UInt64, `country` String, `city_id` UInt64, `city` String, `district_id` UInt64, `district` String, `hash_6` UInt64, `hash_6_coords` String, `hash_7` UInt64, `hash_7_coords` String, `hash_8` UInt64, `hash_8_coords` String, `hash_9` UInt64, `hash_9_coords` String, `country_ru` String, `city_ru` String, `district_ru` String) ENGINE = ReplicatedMergeTree('/clickhouse/tables/shard1/geo_polygons', 'vla-1zwdkyy37cy8iz7f.db.yandex.net') ORDER BY (hash_9, hash_8, hash_7, hash_6) SETTINGS index_granularity = 8192
```

Как загружены данные в таблицу с полигонами

`./olap download-polygons` выгружает данные из YT в необходимом для загрузки в CH виде. В файле не должно быть хедера, порядок колонок должен совпадать с порядком в CH таблице.

```
clickhouse-client --host vla-1zwdkyy37cy8iz7f.db.yandex.net --secure --user geo_user --database geo --port 9440 --password HERE-SHOULD-BE-PASSWORD --query "INSERT INTO geo.polygons FORMAT CSV" --max_insert_block_size=100000 < polygons_msk_spb_ru.csv
```

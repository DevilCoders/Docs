Скрипт для копирования данных в соломон.

Собираем программу:
```shell
ya make noc/grad/cmd/solomon_sensor_syncer
```
Аргументы:
```
usage: solomon_sensor_syncer [-h] [--debug] [--dump] [--token TOKEN] [--max-parallel MAX_PARALLEL] src dst start_ts end_ts

Copy solomon data. See https://a.yandex-team.ru/arc/trunk/arcadia/noc/grad/cmd/solomon_sensor_syncer/README.md

positional arguments:
  src                   data filter
  dst                   target filter
  start_ts              start of a period in unix timestamp or 'auto'
  end_ts                end of a period in unix timestamp or 'auto' (now + 1d)

options:
  -h, --help            show this help message and exit
  --debug               enable debug
  --dump                show rewrite mapping
  --token TOKEN         OAuth token
  --max-parallel MAX_PARALLEL
                        max parallel queries
```

Пример вызова с заменой sensor_name="-" на sensor_name="Relative Humidity 1":
```shell
solomon_sensor_syncer.py --debug 'project="noc", cluster="all", service="service", host="host12*", sensor_name="-"' 'sensor_name="Relative Humidity 1"' auto auto
```
Опция ```--dump``` покажет что будет сделано:
```shell
solomon_sensor_syncer --dump 'project="noc", cluster="shard*", service="net", host="sas1-grad2", sensor="bytes_recv", interface="eth*"' 'interface="eth2"' auto auto

src: {'host': 'sas1-grad2', 'cluster': 'shard83', 'project': 'noc', 'sensor': 'bytes_recv', 'interface': 'eth0', 'service': 'net'}
dst: {'host': 'sas1-grad2', 'cluster': 'shard83', 'project': 'noc', 'sensor': 'bytes_recv', 'interface': 'eth2', 'service': 'net'}
```

Другой пример:
```shell
src: {'host': 'm9-pdu111a', 'cluster': 'all', 'project': 'noc', 'sensor': 'value', 'service': 'pdu_external_sensors', 'sensor_name': '-'}
dst: {'host': 'm9-pdu111a', 'cluster': 'all', 'project': 'noc', 'sensor': 'value', 'service': 'pdu_external_sensors', 'sensor_name': 'Relative Humidity 1'}
```

#### Предостережения

Если указать start_ts = auto, то время берется из solomon из поля createdAt, которое означает время создания серии данных.
Обычно, до этого времени нет данных, но бывают исключение. Например, хост переименовали, а старые данные скопировали.
Тогда, дата создания будет датой начала записи новых данных, а не исторических.

Если нужно удалить данные, то смотри [доку](https://docs.yandex-team.ru/solomon/operations/metrics/deletion).

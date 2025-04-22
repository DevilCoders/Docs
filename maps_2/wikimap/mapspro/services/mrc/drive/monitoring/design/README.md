# Предложение по мониторингу и инвентаризации устройств

## Цели и задачи системы мониторинга

Хотим уметь обнаружать и реагировать на следующие события:
1. устройство сломалось (давно не выходило на связь, хотя должно было)
2. устройство было украдено (выходит на связь, но трек устройства не совпадает с треком автомобиля, на который оно было установлено)
3. устройство плохо функционирует:
    - камера / GPS / LTE / батарея сломались или плохо работают
    - высокая температура
    - высокий cpu_usage
    - мало свободной оперативной/постоянной памяти
    - большое количество крешей приложений
    - большое количество нефатальных ошибок в работе приложений
    - приложение зависает или падает
    - случаются спорадические рестарты устройства

Для понимания, насколько эффективно функционирует устройство в целом, будем использовать отношение суммарной длины сфотографированных целей к суммарной длине посещенных целей.


## Реализация

На клиентских устройствах работает специальное приложение //агент//, которое собирает, сохраняет в постоянную память и выгружает на сервер события и метрики о работе устройства.

На сервере полученные события транспортируются через [logbroker](https://logbroker.yandex-team.ru/docs/) в YT-таблицы. Отдельный фоновый процесс читает данные из YT-таблиц, вычисляет по ним нужные показатели, публикует в базу данных Clickhouse, поверх которой настроены дашборды и мониторинги.


В качестве формата для передаваемых между агентами и сервером сообщений предлагается использовать [Protobuf](https://developers.google.com/protocol-buffers). Это потребует дополнительных усилий в реализации агента для конвертации метрик в целевой формат, вместе с тем это значительно упрощает реализацию и поддержку сервисов, занимающихся обработкой этих логов, поскольку они будут ожидать на входе известный, документированный формат.

Endpoint для выгрузки данных предлагается разместить на стороне мобильной прокси. Это имеет следующие преимущества:
- шифрованный протокол передачи данных
- защита от фрода "из коробки" за счет проверки подписи запросов
- эффективное использование канала мобильной сети за счет протокола HTTP/2

Предполагается, что объем передаваемых данных будет существенно меньше, по сравнению с объемом выгружаемых фотографий, поэтому это не должно создать лишней нагрузки на  мобильную инфраструктуру.


### Протокол взаимодействия

#### Выгрузка метрик POST /mrc/drive/2.x/metrics/upload

Ручка принимает метрики и фрагменты логов.


| **Method** | POST |
|------------|-----|
| **Parameters** |
| deviceid | device identifier |
| **Request Headers** |
| Content-Type | application/protobuf |
| **Request Body** |
| UploadRequest |
| **Response codes** |
| 200 | OK |
| 400 | Bad request |
| **Response Headers** |
| **Response body** |
| Empty |


**Request body**
```c++
message Metric {

    // To be completed
    enum MetricType {
        CPU_USAGE = 0,
        CPU_USER_USAGE = 1,
        CPU_SYSTEM_USAGE = 2,
        MEMORY_TOTAL_BYTES = 10,
        MEMORY_FREE_BYTES = 11,
        DISK_TOTAL_BYTES = 20,
        DISK_USED_BYTES = 21,
        DISK_READ_BYTES = 22,
        DISK_WRITE_BYTES = 23,
        DISK_ROOTFS_TOTAL_BYTES = 30,
        DISK_ROOTFS_FREE_BYTES = 31,
        DISK_ROOTFS_READ_BYTES = 32,
        DISK_ROOTFS_WRITE_BYTES = 33,
        DISK_APPFS_TOTAL_BYTES = 40,
        DISK_APPFS_FREE_BYTES = 41,
        DISK_APPFS_READ_BYTES = 42,
        DISK_APPFS_WRITE_BYTES = 43,
        NETWORK_RECEIVED_BYTES = 50,
        NETWORK_TRANSFERED_BYTES = 51,
        NETWORK_RX_ERRORS = 52,
        NETWORK_TX_ERRORS = 53,
        FIRMWARE_VERSION_ACTIVE = 60,
        FIRMWARE_VERSION_STANDBY = 61,
        SYSTEM_UPTIME = 70,
        CAMERA_ALIVE = 80,
        BATTERY_ALIVE = 90,
        BATTERY_CHARGE_PERCENTAGE = 100,
        TEMPERATURE_CPU = 110,
        APP_ALIVE = 120;
        APP_UPTIME = 121;
    }

    message Aggregate {
        enum AggregateType {
            MIN = 0,
            MAX = 1,
            AVG = 2,
            MEDIAN = 3,
            SUM = 4,
        }

        optional AggregateType type = 1;  // required
        uint32 period_sec = 2;
    }

    optional MetricType type = 1;  // required
    optional Aggregate aggregate = 2;

    oneof scalar_value {
        int64 int_value = 3;
        float float_value = 4;
        string text_value = 5;
        bool bool_value = 6;
    }
}

message MetricWithTime {
    required uint64 timestamp_msec = 1;  // milliseconds since epoch
    repeated Metric metrics = 2;
}


// Describes a fragment from logs of a service
message Log {

    message LogLine {
        required uint64 timestamp_msec = 1;
        required string text_line;
    }

    oneof source {
        string file_path = 1;
        string systemd_unit = 2;
    }

    repeated LogLine log_lines = 3;
}

message UploadRequest {
    repeated MetricWithTime metrics = 1;
    repeated Log logs = 2;
}

```

#### Выгрузка coredump-ов

Поскольку coredump-файлы могут быть внушительного размера, несколько десятков МБ, их рациональнее выгружать частями.

##### POST /mrc/drive/2.x/coredump/upload_start

Создает новую выгрузку.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| deviceid | device identifier |
| **Request Headers** |
| Accept | application/protobuf |
| **Request Body** |
| CoredumpUploadStartRequest |
| **Response codes** |
| 201 | Created |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about created upload |

**Request body**
```cpp
message CoredumpUploadStartRequest {
    required string filename = 1;
    optional uint32 gid = 2;
    optional uint32 pid = 3;
    optional uint32 signal = 4;
    optional uint64 timestamp_msec = 5;
    optional uint32 uid = 6;
}
```

**Response body**
```c++
message CoredumpUploadStartResponse {
    required int64 id = 1;
}
```

##### POST /mrc/drive/2.x/coredump/upload_add_part

Выгружает порцию данных.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| deviceid | device identifier |
| id | upload id |
| part | part id |
| **Request Headers** |
| Content-Length | Size of part in bytes |
| Content-MD5 | MD5-sum for part content|
| **Response codes** |
| 200 | Ok |
| 400 | Wrong upload id |

##### POST /mrc/drive/2.x/coredump/upload_finish

Завершает выгрузку.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| deviceid | device identifier |
| id | upload id |
| **Request Headers** |
| Content-Length | Size of part in bytes |
| Content-MD5 | MD5-sum for part content|
| **Response codes** |
| 200 | Ok |
| 400 | Wrong upload id |


### Реализация приложения-агента

В качестве основы для реализации приложения предлагается использовать open-source решение [FluentBit](https://docs.fluentbit.io). Это open-source проект с лицензией
Apache License v2.0, широко применяется как в embedded-устройствах, так и на серверах.
FluentBit позволяет собирать данные по широкому множеству источников, конвертировать их
в структурированные сообщения, буферизировать их перед отправкой и отправлять их в
различные типы хранилищ, в том числе существует возможность публиковать их по HTTPS.

FluentBit поддерживает два варианта формата для сообщений на выходе: Json, [MessagePack](https://msgpack.org/index.html).

Вот пример реальных данных на выходе FluentBit:
```json
[{"date":1600789984.092267,"Mem.total":16247752,"Mem.used":15891496,"Mem.free":356256,"Swap.total":4194300,"Swap.used":268632,"Swap.free":3925668}]
[{"date":1600789984.119467,"name":"thermal_zone2","type":"TSKN","temp":41},{"date":1600789984.119477,"name":"thermal_zone0","type":"acpitz","temp":25},{"date":1600789984.11948,"name":"thermal_zone7","type":"iwlwifi_1","temp":37},{"date":1600789984.119482,"name":"thermal_zone5","type":"INT3400 Thermal","temp":20},{"date":1600789984.119484,"name":"thermal_zone3","type":"NGFF","temp":34},{"date":1600789984.119487,"name":"thermal_zone1","type":"pch_skylake","temp":41},{"date":1600789984.119489,"name":"thermal_zone8","type":"x86_pkg_temp","temp":42},{"date":1600789984.119491,"name":"thermal_zone6","type":"B0D4","temp":41},{"date":1600789984.119494,"name":"thermal_zone4","type":"TMEM","temp":38}]
[{"date":1600789989.091033,"wwan0.rx.bytes":0,"wwan0.rx.packets":0,"wwan0.rx.errors":0,"wwan0.tx.bytes":0,"wwan0.tx.packets":0,"wwan0.tx.errors":0}]
[{"date":1600789984.136988,"alive":false,"proc_name":"mrc-drive","pid":-1,"mem.VmPeak":0,"mem.VmSize":0,"mem.VmLck":0,"mem.VmHWM":0,"mem.VmRSS":0,"mem.VmData":140199406740393,"mem.VmStk":0,"mem.VmExe":8,"mem.VmLib":24576,"mem.VmPTE":140729195925344,"mem.VmSwap":94229960436848,"fd":0},{"date":1600789989.112133,"alive":false,"proc_name":"mrc-drive","pid":-1,"mem.VmPeak":0,"mem.VmSize":0,"mem.VmLck":0,"mem.VmHWM":0,"mem.VmRSS":0,"mem.VmData":140199406740393,"mem.VmStk":0,"mem.VmExe":8,"mem.VmLib":24576,"mem.VmPTE":140729195925344,"mem.VmSwap":94229960436848,"fd":0}]
[{"date":1600789984.091558,"cpu_p":19.3,"user_p":15,"system_p":4.3,"cpu0.p_cpu":15.6,"cpu0.p_user":12,"cpu0.p_system":3.6,"cpu1.p_cpu":24.2,"cpu1.p_user":18.6,"cpu1.p_system":5.6,"cpu2.p_cpu":18.4,"cpu2.p_user":13.6,"cpu2.p_system":4.8,"cpu3.p_cpu":19,"cpu3.p_user":15.8,"cpu3.p_system":3.2}]
```

Для конвертации сообщений от FluentBit в целевой формат предлагается запустить на агентах дополнительный сервис `MetricsUploader`, который будет слушать на локальном порту и принимать данные по HTTP от FluentBit, конвертировать их в Protobuf и выгружать через мобильную прокси на сервер.

Кроме того, `MetricsUploader` также будет отслеживать появление новых файлов в директории, настроенной для сохранения coredump-файлов, парсить их имена, формировать protobuf-сообщения `Coredump` и также выгружать на сервер.

Один из недостатков такой архитектуры состоит в том, что не получится использовать возможности FluentBit по буфферизации сообщений в постоянной памяти. Эту функциональность либо придется реализовывать самим, либо согласиться с тем, что в период недоступности Интернет часть метрик может быть невыгружена.

### Обработка данных на сервере

#### Отправка данных в Logbroker
Данные, полученные от приложений-агентов, будут сохраняться в YT через [Logbroker](https://logbroker.yandex-team.ru/docs/).
Бэкенд будет принимать в теле запроса данные, содержащие метрики и фрагменты лог-файлов.
Для метрик и логов предлагается завести отдельные топики в Logbroker.
В модели Logbroker-а каждое сообщение имеет порядковый номер, который должен монотоннно возрастать в рамках пары (топик, группа сообщений).
Для одновременной работы нескольких инстансов бэкенда каждый из них на старте должен создавать новую группу сообщений с уникальным именем.
В качестве названия группы можно использовать имя хоста, где работает инстанс, и временную метку с миллисекундной точностью.

Авторизация сервиса в Logbroker будет реализована на базе TVM-тикетов.

#### Сохранение данных в YT с помощью Logfeller
Читателем сообщений из топиков Logbroker-а будет [Logfeller](https://wiki.yandex-team.ru/logfeller/).
Сообщения сохраняются Logfeller-ом в таблицы согласно сконфигурированным временным периодам, например
`//logs/mrc-drive/metrics/1d/`
`//logs/mrc-drive/metrics/1h/`

Также для таблиц конфигурируется период хранения данных по прошествии которого данные будут автоматически удаляться.
Метрики будут сохраняться в shemaful YT-таблице со следующей стуктурой:

**mrc-drive.metrics**
| device_id | timestamp | metric_type | metric_value |
|-----------|-----------|-------------|--------------|
|           |           |             |              |

Логи будут сохраняться в отдельную таблицу:
**mrc-drive.logs**
| device_id | timestamp | source-tag | severity | message |
|-----------|-----------|------------|----------|---------|
|           |           |            |          |         |

#### Отчеты поверх таблиц
Отчеты поверх накопленных данных предлагается создавать в [DataLens](https://datalens.yandex-team.ru/docs/).
В качестве источников данных в DataLens поддерживаются ClickHouse, YT-таблицы, а также ClickHouse over YT (CHYT).
Вариант CHYT позволит строить графики на основе сырых данных, сохраненных в YT.
В качестве альтернативы сырые данные могут быть предобработаны в удобный для представления набор таблиц ClickHouse.
CHYT потребует квоту на заведение собственного вычислительного пула ClickHouse-серверов в YT, называемого кликой (clique).

##### Метрики
Возможны следующие типы чартов, которые возможно строить для любой из метрик:
- График изменения данной характеристики для данного device id на выбранном временном интервале.
- График минимального/среднего/максимального по всем устройствам значения данной характеристики на выбранном временном интервале.
- Графики для top N устройств с минимальным либо максимальным значением данной характеристики на выбранном временном интервале.
- Перцентильные графики (X% устройств имеют данную характеристику не выше Y единиц)

Графики можно строить как по мгновенным значениям данных так и сглаженные, на основе скользящего среднего.

##### Отслеживание активности
- Количество активных устройств по часам / дням.
- Перцентильные графики последней активности устройств (X% устройств последний раз выходили на связь не позднее Y часов назад)
- Таблица с device id, отсортированная по временем последней активности

##### Отслеживание версии прошивки
- Графики изменения количества устройств с каждой версией прошивки на выбранном временном интервале в testing и stable окружениях.
- Таблица с текущей версией прошивки каждого device id, фильтрация по версии, branch или device id

##### Витрина устройств со статусами
Возможен альтернативный вариант представления данных в виде единственной таблицы со списком device id и статусами OK/WARN/CRIT для устройства целиком
либо детально по конкретным характеристикам каждого устройства.
Данные в таблице рассчитываются динамически, можно выбрать интервал времени, по которому строится статистика (напр. за последний час, за последний день).
Для этого потребуется для каждой характеристики вручную установить интервалы значений, соответствующие OK/WARN/CRIT.

Пример:

Time interval: [last hour]
|      device_id   | last activity | cpu usage | memory usage | disk i/o | temperature | mrc app alive | ... |
|------------------|---------------|-----------|--------------|----------|-------------|---------------|-----|
| ae4f7628cbe25312 | OK            | OK        | WARN         | CRIT     | OK          | OK            |     |
| ab410aa44fbcc725 | OK            | OK        | OK           | OK       | WARN        | OK            |     |
| 7d60c3b4130a58f6 | OK            | OK        | OK           | OK       | OK          | OK            |     |

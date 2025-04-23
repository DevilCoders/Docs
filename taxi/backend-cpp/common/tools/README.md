# Утилиты

## postgresql_perf

Утилита для отладки и нагрузочного тестирования драйвера PostgreSQL.

### Параметры запуска
```
  -h [ --help ]                    produce this help message
  -c [ --config ] arg (=pool.json) path to pool config
  -l [ --log-level ] arg (=INFO)   log level (INFO, WARNING, etc.)
  -d [ --duration ] arg (=10)      test duration (s)
  -L [ --long-requests ] arg       use long requests with duration
                                   (s,fractional)
  -I [ --query-interval ] arg (=0) interval between queries (ms)
  -t [ --threads ] arg (=1)        threads count
  -x [ --stop-on-fail ]            stop on worker failure
```

Опция | Описание | Умолчание
------| -------- | ---------
-h,--help | Выводит справочное сообщение выше
-c,--config | Путь к файлу с настройками драйвера | ./pool.json
-l,--log-level | Уровень логирования драйвера (`ALL`, `DEBUG`, `INFO`, `WARNING`, `ERROR`, `NONE`) | INFO
-d,--duration | Продолжительность тестирования (секунды) | 10
-L,--long-requests | Включает использование для нагрузки длинных запросов по X секунд | выкл
-I,--query-interval | Интервал между запросами (в рамках потока) | 0
-t,--threads | Количество потоков для тестирования | 1
-x,--stop-on-fail | Включает остановку теста при возникновении первого необработанного исключения в драйвере (по умолчанию отключается один поток) | выкл

### Формат конфигурационного файла
```json
{
  "ping_interval_s": 2,
  "dead_ping_interval_s": 1,
  "ping_retries": 2,
  "databases": [
    {
      "name": "test",
      "shard_number": 0,
      "type": "master",
      "conn_string": "dbname=test"
    }
  ]
}
```

Конфигурационный файл представляет из себя JSON с полями:

Ключ | Значение | Обязательное?
-----| -------- | -------------
ping_interval_s | Интервал проверки доступности базы (секунды) | –
dead_ping_interval_s | Интервал проверки восстановления доступности базы (секунды) | –
ping_retries | Максимальное количество запросов для уточнения доступности базы | –
databases | Список серверов баз данных, используемых для тестирования (см. ниже) | +

#### databases
Все поля обязательные.

Ключ | Значение
---- | --------
name | Имя базы (сейчас допустимо только `test`)
shard_number | Номер шарда (сейчас допустим только `0`)
type | Тип сервера (`master`, `sync_slave`, `slave`), должен быть уникальным для пары (имя, номер шарда)
conn_string | [Connection string](https://www.postgresql.org/docs/current/static/libpq-connect.html#LIBPQ-CONNSTRING) для подключения к серверу

### Пример использования
```
$ ./postgresql_perf --log-level NONE --duration 9 --long-queries 1.5 --threads 4
tskv    timestamp=2018-01-24 17:29:45,997012    module=SetSystemLogLevel ( common/src/logging/logger.cpp:216 )  level=INFO      thread=7f6bb7cea740    link=None       _type=log       text=Log level will be changed to NONE from INFO

Test statistics: duration=9000ms, failures=0, successes=24, connection errors=0, query errors=0
```

# hermione-usage-stats

Плагин для измерения потребительских метрик hermione (количество запусков, время прогона тестов, ошибки) и сохранения их в БД clickhouse.

## Установка

```bash
$ npm install @yandex-int/hermione-usage-stats --registry=http://npm.yandex-team.ru
```

Подключить плагин в конфиге `hermione`

Минимальный конфиг:
```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-usage-stats': {
            enabled: true,
            project: "web4"
        }
    },

    // ...
};
```

Полный конфиг:
```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-usage-stats': {
            enabled: true,
            project: "web4",
            requestOptions: [
                {
                    protocol: "https:",
                    host: "man-m5a0zu61don9d29n.db.yandex.net",
                    rejectUnauthorized: false,
                    port: 8443,
                },
                {
                    protocol: "https:",
                    host: "vla-4729cn2jora9xcyd.db.yandex.net",
                    rejectUnauthorized: false,
                    port: 8443,
                }
            ],
            db: {
                name: "hermione_local_stats",
                tables: {
                   hermione: "metrics",
                   tests: "tests"
                }
            },
            credentialsSecretName: "sec-01dc1dxehkb9ehssp4tyytz29e",
        }
    },

    // ...
};
```

Параметры:

* enabled - включает или выключает плагин
* project - имя проекта в записях
* requestOptions - массив [опций https.request](https://nodejs.org/dist/latest/docs/api/https.html#https_https_request_options_callback). Если запрос с одним набором опций упадет (например, проводятся работы в ДЦ с хостом), будет использован следующий
* table - имя БД и имя таблицы при запросах
* credentialsSecretName - имя секрета в [секретнице](https://yav.yandex-team.ru/), в котором хранятся логин (поле login) и пароль (поле password) для подключения к БД

## Отладка

Запустить hermione с переменной окружения `DEBUG=hermione-usage-stats:*`

## БД

### Структура

* send_time DateTime - время запроса, заполняется на сервере
* project String - имя проекта
* user_name String - имя пользователя
* session_id Int64 - просто число, чтобы связать между собой запросы в рамках одного запука hermione
* name String - имя метрики
* value String - значение метрики, тип из строки преобразуется на сервере

### Создание
Запрос для создания находится в файле [create_db.sql](./create_db.sql). Создавать БД есть смысл только если вам нужно все свое. В противном случае БД по умолчанию подойдет.
Запрос на создание таблицы нужно выполнить на каждом реплицируемом хосте.

## Графики

Лежат на [дашборде](https://dash.yandex-team.ru/1u0eodva9guuz)

### Добавление нового графика

Добавляем новое поле, которое будет парсить строку в нужный формат, например, `FLOAT([value])`. Добавляем новое поле, которое будет агрегировать это значение, например, `MEDIAN([value_float])`. Теперь поле с медианой можно использовать по оси Y на графиках.

Добавляем новый график, добавляем его на [дашборд](https://dash.yandex-team.ru/1u0eodva9guuz)

## Метрики

При запуске без gui:

* `RUN - AFTER_TESTS_READ` - время от старта процесса до окончания чтения тестов, выполняется всегда первым
* `AFTER_TESTS_READ - SERVER_READY` - время от чтения тестов до открытия GUI, выполняется только при запуске GUI
* `RUNNER_START - FIRST_TEST_START` - время от старта раннера до старта первого теста. При запуске без GUI выполняется почти сразу же после чтения тестов, при запуске GUI - выполняется после запуска тестов из GUI.

Все времена - в секундах.

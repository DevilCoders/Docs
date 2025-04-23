# Тестирования скрипта

## Создание динамических таблиц

Создавать динамические таблицы нужно в тех каталогах, где уже заказан доступ для робота дино.

Например, можно тут: https://yt.yandex-team.ru/hahn/navigation?path=//home/market/users/suddenman

Уже готовые таблицы, например, тут: https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/users/suddenman/profit_index_rearrange

## Запуск скриптов

После изменений скрипта нужно его собрать командой: _ya make_

Аргументы, с которыми можно запускать скрипт лежат в папке _example_. Сами аргументы лежат в _sample\_request\_*_

Перед запуском надо экспортировать ключи для yt и для yql:

```bash
user@host:~/arcadia/market/mars/yql/profit_index_daily$ export YT_TOKEN=<yt_token>
user@host:~/arcadia/market/mars/yql/profit_index_daily$ export YQL_TOKEN=<yql_token>
```

Сам запуск:

```bash
user@host:~/arcadia/market/mars/yql/profit_index_daily$ create_replicated_table/create_replicated_table $(cat example/sample_request_create.txt || tr '\n' ' ')
user@host:~/arcadia/market/mars/yql/profit_index_daily$ fill_profit_index_table/fill_profit_index_table $(cat example/sample_request_fill.txt || tr '\n' ' ')
```

## Дополнительно

Сразу после запуска скрипта записей может не появиться. Чтобы ускорить процесс их появления, следует отмонтировать дин таблицу и примонтировать обратно.

Также при запросах из динамической таблицы без указания limit будут возвращаться не все данные, так что лучше явно его указывать, чтобы убедиться в правильности наполнения таблицы вашим скриптом.


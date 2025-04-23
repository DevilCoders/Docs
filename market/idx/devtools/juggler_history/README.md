# Анализатор вечно красных мониторингов

Получает из Juggler-API все изменения статусов алерта и выводит их в виде таблицы. Поддерживает 2/3 Python, и может работать
без аркадийной сборки.

## Примеры запуска
```(bash)
python main.py --project market.datacamp --tags market_indexer_datacamp market_testing
Processing mi-datacamp-united-testing routines-saasdiffbuilder-status
Since: 2022-02-22 13:53:20
Until 2022-02-22 20:53:20
╒════╤════════════════════════════╤═════════════════════════════════╤═════════════════╤════════════════╤════════════════╕
│    │ Host                       │ Service                         │ Crit time       │ Warn time      │ Ok time        │
╞════╪════════════════════════════╪═════════════════════════════════╪═════════════════╪════════════════╪════════════════╡
│  0 │ mi-datacamp-united-testing │ routines-saasdiffbuilder-status │ 6:33:20(93.65%) │ 0:00:00(0.00%) │ 0:00:00(0.00%) │
╘════╧════════════════════════════╧═════════════════════════════════╧═════════════════╧════════════════╧════════════════╛
```

Аргумент `--tags` можно указывать несколько раз.
Такой селекктор на дашборде например `(tag=market_production & tag=market_indexer_datacamp) | (tag=market_prestable & tag=market_indexer_datacamp)`
Эквивалентем такому запуску:
```(bash)
python main.py --project market.datacamp --tags market_production market_indexer_datacamp --tags market_prestable market_indexer_datacamp
...
```

## Как запустить в sandbox
1. Копируем таску [https://sandbox.yandex-team.ru/task/1224663787/view](https://sandbox.yandex-team.ru/task/1224663787/view)
2. Указываем нужный проект и теги мониторингов в `program_args`
3. Вывод программы лежит в ресурсе `log1`, файлик `program.out.txt`

### TODO
* FEATURE: Вставлять ссылки на juggler
* FEATURE: Обрабатывать алерты в несколько потоков
* BUG: Не учитывается самый старый статус алерта из-за фильтра по since
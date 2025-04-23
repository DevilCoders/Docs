# Export to YT
В sandbox по расписанию раз в сутки (8:00) запускается задача, которая:
1. ходит в комбинатор и получает инфу по берушным постоматам (локерам)
2. записывает эти данные в YT

## Результаты
1) [Последняя таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/combinator/export/beru_lockers/latest)
2) [Все таблицы](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/combinator/export/beru_lockers)

## Sandbox
1. [sheduler](https://sandbox.yandex-team.ru/scheduler/43694/view)
2. [source](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/market/combinator/ExportBeruLockersToYt/__init__.py)

## Разработка
1. пишем код в этой библиотеке
2. тестируем на запуске бинарника `export_to_yt`
3. собираем и загружаем бинарный таск в sandbox:
```sh
manushkin@laptop:~/src/arcadia/sandbox/projects/market/combinator/ExportBeruLockersToYt$ ya make -r
manushkin@laptop:~/src/arcadia/sandbox/projects/market/combinator/ExportBeruLockersToYt$ ./bin/export_beru_lockers_to_yt upload --attr release=stable --attr task_type=EXPORT_BERU_LOCKERS_TO_YT
```

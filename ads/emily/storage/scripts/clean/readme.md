# Cleaning Tool

Чистилка Emily Storage.

## Использование

```bash
# Собрать
ads/emily/storage/scripts/clean$ ya make -r
```

```bash
--key TEXT                  Ключ модели
--version TEXT              Версия модели
--all-except-versions TEXT  Удалить все кроме указанных версий
--config TEXT               Взять модели из конфига
--indexer-config TEXT       Удалить модели, которых нет в валидационном конфиге
--start-from-version TEXT   Начать очистку начиная с версии
--less-than-version TEXT    Начать очистку моделей до версии
--created-before-date TEXT  Начать очистку моделей созданных до указанной даты
--dumps                     Удалить все обезглавленные дампы
--prod / --dev              Environment Type
-T, --transport TEXT        Transport Status [draft|new|valid|invalid|rejected]  [default: draft]
-U, --upload TEXT           Upload Status [ready|not_ready|broken|deleting|no_dumps|deleted]  [default: ready]
--owner TEXT                Владелец ресурса
--deduplicate               Удалить дубликаты
--with-meta                 Удалить все дампы включая мету
--with-head                 Удалить все дампы включая мету и сам head
--dry-run                   Тестовый запуск, без удаления
--prompt                    Спрашивать перед удалением
-h, --help                  Show this message and exit.

ads/emily/storage/scripts/clean$ ./clean --help
```

## Конфиг

```json
{
    "models": [
        {
            "key": "ключ модели",
            "version": "версия модели (optiona)",
            "versions": "версии модели (optiona)",
            "start_from_version": "начать очистку начиная с версии (optiona)",
            "less_than_version": "начать очистку версий до версии (optiona)",
        },
        ...
    ]
}
```

```bash
ads/emily/storage/scripts/clean$ ./clean --config path_to_config.json --dry-run --with-meta -T valid
```

## Удалить дубликаты

```bash
ads/emily/storage/scripts/clean$ ./clean --key lolita3_maxdepth_unstable_7days_top20_v3 --version 2014-11-16T00:00:00 -T draft --prod --with-head --deduplicate
```

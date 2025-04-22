# Создание таблиц в YT

Для создания табличек в YT можно использовать скрипт [yt_create_table.py](https://a.yandex-team.ru/arc/trunk/arcadia/adv/tools/yt/create_table/yt_create_table.py)

Зачем понадобился скрипт:
* умеет создавать таблицу по json.schema — можно создать таблицу по нескольким путям запустив одну и туже команду с разными путями;
* умеет создавать реплицируемую таблицу одной командой, сразу во всех указанных кластерах.

Для создания таблицы для теста, где-нибудь в tmp не надо вспоминать как это делается, достаточно почитать хелп к сприпту.
Скрипт есть на ppcdev-ах и ppcback-ах, а значит его можно использовать для создания таблиц с помощью миграций в продакшене, т.к. на ppcback-ах есть необходимые секреты;

Пример использования
```bash
YT_TOKEN=`cat /etc/direct-tokens/yt_robot-direct-yt` yt_create_table --cluster $CLUSTER --table <//home-путь-к-таблице> --schema-file <файл со схемой.json>
```

Пример схемы: [DirectBannerResources.schema.json](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/bstransport-yt/schemas/DirectBannerResources.schema.json)

## Реплицируемые таблицы
[Общее отписание](https://docs.yandex-team.ru/yt/description/dynamic_tables/replicated_dynamic_tables)

Пример команды для создания
```bash
YT_TOKEN=`cat /etc/direct-tokens/yt_robot-direct-yt` yt_create_table -r --cluster $MASTER_CLUSTER --replica-clusters $SLAVE_CLUSTER1 $SLAVE_CLUSTER2 --table <//home-путь-к-таблице> --schema-file <файл со схемой>
```

## Собрать пакет
см. [README.md](https://a.yandex-team.ru/arc/trunk/arcadia/adv/tools/yt/create_table/README.md)

## Миграции

[описание в разделе про миграции](../../jeri/guide/yt-create-table-migr.md)





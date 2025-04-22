MBI PARTNER-STAT (аналитические отчеты для партнеров Маркета)

## Разработка
Разработка идет в arc. Настройка arc: https://wiki.yandex-team.ru/arcadia/arc/
1. Создать проект для Idea: `ya ide idea -r /Users/batalin/IdeaProjects/mbi-partner-stat -l /Users/batalin/arc/arcadia/market/mbi/partner-stat --iml-in-project-root`

## Локальное тестирование с YT
1. Прочитать про запуск тестов с YT тут https://wiki.yandex-team.ru/users/varkasha/java-yt-local/
2. Если хочется запустить тесты из идеи нужно перейти в Run -> Edit Configurations... Выбрать там JUNIT и прописать в Environment variables YT_PROXY=<адрес до локального YT>
Для локального тестирования нужно писать тесты аккуратно и подчищать данные=

## Локальный запуск (без TVM)
Для локального запуска необходимо:
1. Поднять локально Postgres и Clickhouse. Можно воспользоваться докером `stub/docker-compose.yml`
2. Чтобы подключить гео базу (встроенный словарь) - запустить скрпит src/clickhouse/link_geo_base.sh
3. Перезапустить контейнеры.
4. Накатить на локальную базу init-скрипт из `src/liquibase/local/init_db.sql`
5. Накатить liquibase. Для этого запустить `python liquibaseDev.py update`
6. Создать файл `src/main/properties.d/local/application-local.properties`. за основу взять `application-local.properties.sample`
7. Добавить VM-options для запуска `-Dconfigs.path=/path/to/partner-stat/src/main/properties.d`, указав свой путь

## Локальный запуск (с TVM)
Если хочется запустить проект с рабочим tvm,
то надо повторить пункты 1-5 из запуска без TVM. После этого:
1. Указать в `application-local.properties`: `mbi.partner_tvm.tvm2.client_id` - id клиента приложения,
`mbi.partner_stat.tvm2.secret` - секрет приложения,
`mbi.partner_tvm.tvm2.allowed_client_ids` - список разрешенных id клиентов
2. Включить tvm в `application-local.properties`: `mbi.partner_tvm.tvm2.enabled=true`

## Отладка с TVM
Подробнее про отладку: https://wiki.yandex-team.ru/passport/tvm2/debug/

Для отладки пригодится tvmknife. Его можно собрать самому из аркадии
1. Собираем `ya make -r passport/infra/tools/tvmknife -o /tmp/tvmknife`
2. Переносим в удобное место. При необходимости добавляем alias

Через tvmknife можно сгенерировать tmv-тикет, если знаете секрет сервиса:
1. Заходим в список ресурсов. Например: https://abc.yandex-team.ru/services/mbidevops/resources/
2. Тыкаем на нужный, узнаем его clientId и секрет
3. Генерируем tvm-тикет `tvmknife  get_service_ticket client_credentials -d DESTINATION_ID -s SOURCE_ID -S SOURCE_SECRET`
4. Тикет надо передать в заголовке `X-Ya-Service-Ticket`. Это сервисный тикет.
Пользовательский мы не поддерживаем. Не нужен пока что

## Настройка подключения к ClickHouse
Если есть доступ к тестовому кластеру КХ - просто указываем их в `application-local.properties`:
`mbi.partner_stat.clickhouse.hosts, mbi.partner_stat.clickhouse.user, mbi.partner_stat.clickhouse.password`.
Хосты до тестинга можно взять из `application-testing.properties`

Если доступа к тестовому КХ нет, то надо поднять локально свой кластер.
Можно сделать это с помощью докера: https://hub.docker.com/r/yandex/clickhouse-server/

Другие способы, как можно поднять кластер КХ, есть на оф.сайте: https://clickhouse.yandex/docs/en/getting_started/

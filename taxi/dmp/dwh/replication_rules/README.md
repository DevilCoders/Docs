## Правила репликации
* [Чат поддержки](https://wiki.yandex-team.ru/taxi/backend/datastorage/#chatpodderzhki)
* [Документация](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/how_to_start)
* Правила репликации лежат тут: **dwh/replication_rules/replication_rules**
* [Генерация правил](#генерация-правил): быстрое создание для api/pg/mysql/mongo.

## Тесты

```
make test
```
Нужен **backend-py3** со всеми сабмодулями по относительному пути ../../backend-py3.
Путь можно указать явно переменной окружения **BACKEND_PY3**.

```
BACKEND_PY3=/abs/path/to/backend-py3 make test
```

## Code linters
* Быстрая установка зависимостей: `make install-deps`
* Форматирование до коммита: `make smart-format`
* Если закоммитили с неправильным форматированием: `make format`
* Включены следующие форматтеры: **taxi-yamlfmt**, **taxi-black**, **taxi-jsonfmt**. [Подробнее](https://github.yandex-team.ru/taxi/code-linters#code-linters)

## Генерация правил
### Быстрый старт

* Установка зависимостей: `make install-deps` (если установлен `taxi-python3` - запускайте через него)
* Подробнее про допустимые аргументы: `python3 rules_generator --help`
* Больше логов: `python3 rules_generator <command> --debug`
* Если вы не из такси, то стоит проверить есть ли у вас правило доступа до `replication.taxi.tst.yandex.net`
  в [панчере](https://puncher.yandex-team.ru/?rules=exclude_rejected&values=all&sort=creation_time). В поле `Источник`
  укажите себя как на стаффе. В поле `Назначение` укажите `replication.taxi.tst.yandex.net`. Если доступ есть, то
  вы увидите правило [вида](https://puncher.yandex-team.ru/?id=5bc971a8d5626dfd0a22d377). Если нет, то нажмите на
  кнопку `Создать заявку на правило`. Затем в поле `Источник` укажите либо себя, либо свою группу. В поле `Назначение`
  укажите `replication.taxi.tst.yandex.net`.

Пример:
```
python3 rules_generator --source mysql --tables analytics.webim_chat_departments --namespace eda --secret-source MYSQL_EDA_EDA_ANALYTICS_DWH_EXPORT
```

### Аргументы запуска
* `--source: [postgres/mongo/mysql/oracle/api]`: тип источника
* `--tables`: полное имя таблицы со схемой, например `analytics.webim_chat_departments`. Для монги формат такой: `--table database.collection`. Для **api** ничего указывать не нужно
* `--secret-source <STRONGBOX_ID>`: алиас из `config.yaml`: STRONGBOX_ID или yav alias.
* `--yav-secret-register <sec-123testing>`: создаст алиас секрета в `config.yaml`. Нужно только для добавления нового секрета типа yav.
    Можно указать сразу с продакшен секретом: `--yav-secret-register sec-123testing/sec-345production`
* `--namespace [market/eda/taxi/см. --help]`: пытается определиться автоматически, но лучше задавать явно. Влияет на определение пути в yt, на префикс правил.
* `--responsible <group>`: группа ответственных за мониторинг поставки
* `--scale [tiny/middle/large]`:- размер источника для определения партиционирования raw/raw_history:
    tiny: таблица до 1Gb, raw - не партиционируем, raw_history - по годам
    middle: таблица до 100Gb, raw - по годам, raw_history - по месяцам
    large: таблица более 100Gb, raw/raw_history - по месяцам
* `--options [msk_timezone, prepared_statement_disabled]` : - переопределение опций подключения к источнику:
    prepared_statement_disabled - отключить проверки через prepared statements в postgres
    msk_timezone - указать, что все даты в таблице лежат в UTC+3
* `--scope <name>`: фактически имя директории, в которой будет лежать правило. Пытается определиться автоматически, но иногда для читаемости имеет смысл задать явно
* `--snapshot`: указать, что поставка снапшотом, а не инкрементами
* `--replicate-by`: указать поле для репликации инкрементом.
    Если не задан `--snapshot` и `--replicate-by`, генератор будет искать поле по списку типовых имен
* `--created-by`: указать поле с датой создания записи - для партиционирования.
* `--rewrite-rule`: если нужно перегенерировать уже существующее правило целиком.
* `--with-ext`: если нужен читатель для ODS.


### На что обращать внимание
1) Путь файла. Одна таблица = одно правило = один файл .yaml
Имя папки должно начинаться со слова имени вашего неймспейса (кроме такси, как примеры: eda/market), чтоб было проще искать.
Генератор сразу генерит правило по условно правильному пути, но иногда есть смысл сократить, а лучше сразу передать генератору `--rule-name <namespace>_<source_name>_<table>` , тогда файл будет `replication_rules/<namespace>_<source_name>/<table>`.
По умолчанию все правила лежат в модуле replication_rules, по пути `replication_rules/<namespace>_<source>`, например market_mbi.

2) `replication_type: queue` , если вы хотите забирать по инкременту. иначе - `queue_snapshot`. Автоматическая генерация может допустить ошибку.
Если есть `updated_at` или похожее поле, либо явно задано `--replicate-by`, сгенерируется правило с инкрементом. Либо можно явно задать `--snaphot`

3) Дополнительные опции:
    - `--options prepared_statement_disabled ` - нужно для репликации из postgres: если pgbouncer не поддерживает `prepared_statement`, тогда при старте правила будет ошибка. В правиле: `prepared_statement_disabled: true`
    - `--options msk_timezone `, в правиле: `timezone: Europe/Moscow` - если в ваших источника стоит время в MSK (+3) без таймзоны

4) YT `prefix: <...>` определяет путь на YT, по умолчанию может выставиться неправильный префикс. Лучше всего ставить правильный `--namespace`, а потом менять префикс руками при необходимости.


### Документация
Тулза для создания правил репликации. Её шаги:

1. Создание правила с источником.

    Источник необходимо указать в параметре `--source`.

    Поддерживаемые типы источников:
    * postgres: достаточно указать `--tables` и `--secret-source`
    * mysql: достаточно указать `--tables` и `--secret-source`
    * api: тут нужно передавать следующие аргументы:
        * `--rule-name`
        * `--scope`
        * `--created-by` и `--replicate-by` (если он есть).
           Для репликации не по дате для api пока нет полноценной поддержки
        * `--primary-keys` - это нужно для сырых слоев
    * mongo: здесь необходимо передавать аргументы:
      * `--tables` - как **database.table**, где database и table - это соответственно
      * `--database` - это ключ в секдисте.  Например, если в секдисте подключение лежит так:
        ```
        {
            "mongo_settings": {
                "my_database": {
                ...
                },
                "accepted_eulas": {
                ...
                },
                ...
            },
            "postgres": {
                ...
            },
            ...
        ```
        то нужно указать `--database my_database`
      * `--replicate-by` или `--snapshot` (одно из двух).
    * oracle: достаточно указать `--tables` и `--secret-source`
       tables, replicate_by, primary_keys могут быть как в lower так и в uppercase - генератор поправит

    Примеры запуска:
      - Для **strongbox**: `python3 rules_generator --source postgres --secret-source POSTGRES_EDA_EATS_TAGS --tables db.tags_replica --primary-key provider`
      - Для **yav**: `python3 rules_generator --source mysql --tables modx_web_users_org --secret-source eats_tips --yav-secret-register sec-01fzadwxwbwycj0nryge8fvkmh`

2. Создание сырых слоев YT.
    * [Почему их обязательно нужно создавать](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/generated-targets#dollarraw)
    * Их также нужно выкатить в тестинг и прод и инициализировать
    * Есть 2 типа таргетов:
        * {rule_name}_raw - сырые данные как есть, этот слой должен быть всегда. Обычно партицируется по `--created-by` по годам.
        * {rule_name}_raw_history - история изменений. Если этот таргет есть, но не работает, его можно удалить, если он вам не нужен.
    * Выбираемые по дефолту префиксы и пути **dwh-rules/eda-dwh** - нужно оставить как есть, это позволит прорасти вашим правилам для дальнейшего процессинга dwh и аналитики.

3. [Опционально] Создание структурированных yaml (это не ODS, а нативные для репликации структурированные слои).
    * Тут нужно больше зависимостей: используйте `taxi-python3` или `make install-generator-deps-all`
    * Используйте флаг `--yt-struct` дополнительно к основным
    * Можно поправить дефолтные касты в /rules_generator/config.yaml (но не нужно это коммитить)
    * Если хотите исключить какие-то поля, то укажите `--excluded-fields` и перечислите названия
      исключаемых полей через пробел

4. [Опционально] Добавление индексов.
   * В YT нет встроенных индексов, поэтому приходится джойнить таблицы руками
   * Чтобы облегчить задачу, запустите тулзу и воспользуйтесь опцией `--yt-indexes`
   * Формат запуска: через пробел перечислите индексы, в каждом индексе через запятую перечислите колонки
   * Пример: `python3 rules_generator --source postgres --tables products.virtual_categories_subcategories --yt-indexes virtual_category_id,subcategory_id virtual_category_id,rank`
   * В yaml файлах с описанием правил появится специальный маппер `$index`, который
     будет хранить информацию об индексах


Пример максимально подробного запуска команды для postgres
`python3 rules_generator --source postgres --secret-source market_logistics_management_service
--tables logistics_point --rule-name my_cool_logistics_point --replicate-by updated_at
--scope market_lms --options msk_timezone prepared_statement_disabled
--scale middle --namespace market --responsible market --with-ext`

Пример для oracle
`python3.7 rules_generator --source oracle --rule-name my_cool_rule  --namespace market
--scale large --debug --replicate-by eventtime --with-ext
--options msk_timezone --secret-source market_mbi
--table=market_billing.v_yt_exp_daily_completions --primary-keys campaign_id`

В некоторых случаях эти правила могут создаваться некорректно, их нужно редактировать руками.
В этом, и других случаях, если что-то не заработало как ожидалось: обратитесь
[в чат поддержки репликации](https://wiki.yandex-team.ru/taxi/backend/datastorage/#chatpodderzhki),
приложив при этом все логи запуска с флагом `--debug`.

### Как тулза генерации работает?
1) Тестинг репликации собирает в себе всю информацию про схемы по крону (для этого нужны коннекты в секдисте).
2) У тестинга репликации есть API, которое предоставляет информацию про эти схемы по запросу.
3) Тулза запускается локально и ходит в это API для обработки схем.


### Возможные проблемы:
   * Если процесс генерации правила падает с ошибкой `TimeoutError: [Errno 60] Operation timed out` - значит нет
     доступа до `replication.taxi.tst.yandex.net` по порту `80`. Чтобы решить эту проблему
     надо в [Puncher](https://puncher.yandex-team.ru/?rules=exclude_rejected&values=all&sort=source) создать заявку.

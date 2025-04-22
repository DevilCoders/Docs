
Архитектура словарей описана на [wiki страничке](https://wiki.yandex-team.ru/Market/Projects/marketstat/yt/dicts-delivery).

Как добавить загрузку в YT нового словаря
=========================================

Note: Убедитесь, что его еще нет в
[//home/market/production/mstat/dictionaries](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/market/production/mstat/dictionaries)

Загрузку словаря из источника осуществляет loader. Если загруженное из источника нужно специфично распарсить,
то понадобится parser (который нужно будет реализовать).


**Типовая загрузка словаря**: выгрузка данных из базы (pg,oracle,mysql etc) по jdbc 1 или более раз в сутки - без необходимости пост-обработки и обогащения этих данных.
Для такой выгрузки подходит готовый jdbc-загрузчик, нужно только добавить нужные параметры в конфиг

Новые правила поставки данных
---------------------------------
В соответствии с [договорённостями](https://wiki.yandex-team.ru/Market/Projects/marketstat/dwh/Postavka-novyx-dannyx-v-edinoe-xranilishhe-Marketa/) поставка новых данных
ложится на плечи системы-источника.
В числе прочего предполагается, что новые загрузки хранятся в квоте источника и мониторятся им.

Таким образом, помимо стандартной процедуры добавления загрузки необходимы следующие шаги:

1) Система-источник в своем аккаунте на YT создает директорию dictionaries на Hahn и Arnold
```
Пример: рассмотрим условную систему "market-abc", чьи данные в YT лежат тут:

//home/market/production/abc/.. (в аккаунте "market-abc")
//home/market/testing/abc/.. (и аккаунте "market-abc-test")

Нужно создать по 2 директории на 2х кластерах (прод и тестинг, Хан и Арнольд):

//home/market/production/abc/dictionaries (или далее в подпапках //home/market/production/abc/../dictionaries)
//home/market/testing/abc/dictionaries (или /home/prestable/market/abc/dictionaries)
```

2) Система-источник выдает роботам robot-market-dicts и robot-market-dict-ts необходимые доступы
  ```
 В данном примере:

 robot-market-dicts:
 use:  "market-abc" HAHN + ARNOLD
 read/write/remove: //home/market/production/abc/dictionaries HAHN + ARNOLD

 robot-market-dict-ts:
 use:  "market-abc-test" HAHN + ARNOLD
 read/write/delete: //home/market/testing/abc/dictionaries HAHN + ARNOLD
```

3) Система-источник обращается к дежурому мстат (на переходный период) и просит создать папку-симлинку:
 ```
 //home/market/production/abc/dictionaries ==> //home/market/production/mstat/dictionaries/abc (HAHN + ARNOLD)
 //home/market/testing/abc/dictionaries ==> //home/market/prestable/mstat/dictionaries/abc (HAHN + ARNOLD)
```

4) Не забыть в конфиге новых загрузок указать свою подпапку в destination
```
abc:
  - source: ABC_DB.dict1
    destination: abc/dict1
  - source: ABC_DB.dict2
    destination: abc/dict2
```

Использование готового загрузчика
---------------------------------
### jdbc
Загружает таблицу из указанной базы данных.
Если нужно загрузить все поля таблицы или можно обойтись SQL запросом без параметров, то для этого достаточно добавить запись в
[конфиг](src/main/resources/configs/jdbc-dictionaries.yaml).

В противном случае придется кастомизировать, для примера можно посмотреть
 * [QueryMultipleShardsJdbcLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/jdbc/QueryMultipleShardsJdbcLoader.java)

Упрощенная процедура добавления типовой выгрузки по jdbc
------------------------------------------
Для того, чтобы добавить новую типовую выгрузку по jdbc

1) **Ответить на вопрос**: из данного источника (база+схема) уже поставляются другие словари?
посмотреть можно здесь:
[dictionaries-yt-production.properties](src/main/properties.d/production/dictionaries-yt-production.properties)

2) Подготовить ПР с изменениями в
[jdbc-dictionaries.yaml](src/main/resources/configs/jdbc-dictionaries.yaml) и [dictionaries-yt-production.properties](src/main/properties.d/production/dictionaries-yt-production.properties) (если новый источник)
и призвать в ПР дежурного разработчика МСТАТ

3) Протестировать в [integration-test](src/integration-test/README.md))

### Добавление нового словаря из источника, в который уже ходим
В источник уже ходим, т е для него есть конфиги вида dictionaries.loaders.<имя_источника>.jdbc.*
Тогда нужно просто добавить в список таблиц, забираемых из этого источника, новые таблицы
```
<имя_источника>
  - source: my_new_table
 ```
Например: [checkouter](src/main/resources/configs/jdbc-dictionaries.yaml?rev=4354770#L394)


### Добавление словаря из нового источника:
1. убедиться, что до системы-источника есть дырки
```
из прода словарей:
_GENCFG_SAS_MARKET_PROD_MSTAT_DICTIONARIES_
_GENCFG_VLA_MARKET_PROD_MSTAT_DICTIONARIES_
из тестинга словарей
_GENCFG_SAS_MARKET_TEST_MSTAT_DICTIONARIES_
_GENCFG_VLA_MARKET_TEST_MSTAT_DICTIONARIES_
```

2. Прописать конфиг подключения к источнику (вида dictionaries.loaders.<имя_источника>.jdbc.*) в
[dictionaries-yt-production.properties](src/main/properties.d/production/dictionaries-yt-production.properties),
[dictionaries-yt-testing.properties](src/main/properties.d/testing/dictionaries-yt-testing.properties)
и
[dictionaries-yt-development.properties](src/main/properties.d/development/dictionaries-yt-development.properties) (можно скопировать из теста)

Полный список пропертей:
```
dictionaries.loaders.<имя_источника>.jdbc.driver=
dictionaries.loaders.<имя_источника>.jdbc.url=
dictionaries.loaders.<имя_источника>.jdbc.schema=
dictionaries.loaders.<имя_источника>.jdbc.username=
```
<имя_источника> - любое, главное чтоб совпадало с тем, что в [jdbc-dictionaries](src/main/resources/configs/jdbc-dictionaries.yaml?rev=4354770#L394)

3. Также нужен пароль ```dictionaries.loaders.<имя_источника>.jdbc.password``` для прода и тестинга, он прописывается в секретных датасорсах РТС контейнера, для этого нужно прислать их по почте дежурному мстат и попросить добавить

4. В [jdbc конфиге](src/main/resources/configs/jdbc-dictionaries.yaml?rev=4354770#L394) добавить выгрузку из источника
```
<имя_источника>
  - source: <имя таблицы на источнике>
 ```
### Если в источнике есть поле date
`date` - системное поле в словарях и если его не заменить, будет путаница.
Пример переименования поля:
```
rename
  date: <новое имя для поля в YT>
```
### Подробнее про jdbc-конфиг

**Минимально необходимый конфиг**:
```
<имя_источника>
  - source: <имя таблицы на источнике>
 ```
он создаст выгрузку в одноименную таблицу на YT в [корневую директорию dictionaries](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries), выгрузка будет проходить раз в сутки.
Будут выгружаться все поля из источника под оригинальными именами.
Tипы полей - адаптация типов из источника в типы YT

**Максимально возможный конфиг**:
```
source: <имя таблицы на источнике>
destination: <подпапка>/<имя таблицы в ыте>
cast:
    <имя поля на источнике>: <новый тип для YT>
    <имя поля на источнике 2>: <новый тип>
description: <Человекочитаемое описание словаря>
startDate: <Дата, с которой нужно загрузить историю, по дефолту - день выезда конфига в прод>
rename:
      <имя поля на источнике>: <новoе имя для YT>
loadPeriodHours: <Раз в сколько часов перезагружать словарь, по дефолту 24>
modificationTime: <Выражение для определения времени изменения источника. Если задано, то каждый час проверяем наличие изменений и если были - перевыгружаем>
conversionStrategy: LEGACY //для новых словарей не нужно
loadTimeoutMinutes: <Значение таймаута в минутах, по-умолчанию 12 часов>
transactionIsolation: один из четырёх уровней изоляции, см. TransactionIsolation.java
sortBy: [<column_name>...] список колонок, по которым будет отсортирована таблица (в порядке перечисления); по-умолчанию список пустой и сортировка не выполняется
ttlDays: По умолчанию для дневных выгрузок хранение бессрочно, но крайне рекомендуется определять и выставлять TTL таблицам на yt (можно указать ttlDays в конфиге). Для часового скейла TTL обязателен (по умолчанию - 3 дня)
allowEmpty: [true/false, default:false] признак, что выгрузка может быть пустой и это не ошибка
        (будет создаваться пустая таблица, если не указано skipEmpty)
skipEmpty: [true/false, default:false] признак, что выгрузка может быть пустой,
        но если она пустая, её не нужно публиковать на YT - создавать таблицу и отсылать step-event
        (нужно в специфических кейсах, когда дальнейшие потребители не умеют жить с путыми таблицами)
```

Пример:
```
mbi:
  - source: market_billing.campaign_info
    conversionStrategy: LEGACY
  - source: market_billing.mbi_super_view
    destination: mbi/mbi_super
    cast:
      some_money_flag: string
    rename:
      money_outdated: money_old
    description: Данные из биллинга про какие-то деньги
    startDate: 2019-02-01
    loadPeriodHours: 4
    conversionStrategy: LEGACY //для новых словарей не нужно
    modificationTime: sql(select max(modification_date) from market_billing.mbi_super_view)
    loadTimeoutMinutes: 180
    sortBy: [mbi_id, modification_date] // таблица будет храниться отсортированной по 1:mbi_id, 2:modification_date
    ttlDays: 60
    allowEmpty: false //это значение по умолчанию, можно не указывать. если выгрузка пуста,
       таблица не будет создана, зажжется мониторинг
```

[Пример ПР на добавление словарей из новых источников](https://a.yandex-team.ru/review/732515)


Создать свой загрузчик словарей по аналогии
------------------------------------------
Нужно будет создать бин загрузчика в [LoadersConfig](src/main/java/ru/yandex/market/stat/dicts/config/LoadersConfig.java)
или же реализовать свой загрузчик и пометить spring-аннотацией @Component
(как [GeobaseLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/GeobaseLoader.java)).

### http
[HttpLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/HttpLoader.java) загружает данные по http.
Например, можно загружать данные из mds, как это делается для
[shop_ratings](src/main/java/ru/yandex/market/stat/dicts/config/LoadersConfig.java#L211).
Или же просто по http, как [regions (geobase)](src/main/java/ru/yandex/market/stat/dicts/loaders/GeobaseLoader.java)

При этом придется написать свой парсер, для интерпретации загруженных данных (придания типа, названия колонок и т.п.)

### market-data-getter
[MarketDataGetterLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/MarketDataGetterLoader.java)
загружает из локальной файловой системы данные, которые поставляюся
[market-data-getter](https://wiki.yandex-team.ru/Market/Development/getter)-ом.

Этот вариант самый трудоемкий по тестированию, так как нужно на свой ноутбук для отладки загрузить эти данные
(см. раздел "Как тестировать словарь из market-data-getter" в [integration-test](src/integration-test/README.md))
Для примера можно посмотреть
 * [SkuLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/SkuLoader.java),
 [ModelsLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/ModelsLoader.java) и
 [ParametersLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/ParametersLoader.java),
 загружающие данные из protobuf-ок.
 * [shops](src/main/java/ru/yandex/market/stat/dicts/config/LoadersConfig.java#L245),
 [shops_outlet](src/main/java/ru/yandex/market/stat/dicts/config/LoadersConfig.java#L298),
 загружающие данные из обычных текстовых файликов с кастомным парсером или json/xml


Написание своего загрузчика
---------------------------
Если у вас совершенно новый источник, из которого словари доселе не загружались,
то вам придется реализовать свой загрузчик, реализовав интерфейс
[DictionaryLoader](src/main/java/ru/yandex/market/stat/dicts/loaders/DictionaryLoader.java).
Тут необходимо помнить концепт, что загрузчик загружает данные, а интерпретацией данных занимаются парсеры.
Парсер должен реализовывать интерфейс
[DictionaryParser](src/main/java/ru/yandex/market/stat/dicts/parsers/DictionaryParser.java).
Все парсеры регистриуются в
[ParsersDictsConfig](src/main/java/ru/yandex/market/stat/dicts/config/ParsersDictsConfig.java).

В качестве примера добавления словаря можно просмотреть
[список закрытых pull-request-ов](https://github.yandex-team.ru/market-java/marketstat/pulls?q=is%3Apr+is%3Aclosed)


Что делать, если я не умею / думаю, что не получится / нет ресурсов для этого?
------------------------------------------------------------------------------
Можно создать тикет в [MSTAT](http://st.yandex-team.ru/MSTAT), списаться с
[координатором](https://wiki.yandex-team.ru/market/projects/marketstat/#komanda)
и, объяснив свою ситуацию, договориться о сроках.


Как добавить/удалить/изменить поля в уже загружающемся словаре?
===============================================================
Для этого достаточно найти загрузчик словаря, просмотреть как он загружает и поправить в нужном месте.
Но! Мы стремимся к тому, чтобы словарь загружал автоматически все поля, которые есть в источнике
(как правило это легко добиться в jdbc источниках).


Как организовать поставку словаря в ClickHouse
==============================================
Словари в ClickHouse поставляются двумя способами:
 * Исторический словарь - таблица в ClickHouse, с полем day (партиционированна обычно по месяцам).
 * Неисторический словарь - [внешний словарь в ClickHouse](https://clickhouse.yandex/docs/ru/dicts/external_dicts)

### Поставка исторических словарей

По историческим причинам компонент Dictionary занимается отгрузкой словаря в ClickHouse.
Скоро он передаст свои полномочия
[clickhouse-dealer](https://github.yandex-team.ru/market-infra/market-health/tree/master/clickhouse-dealer).
Но пока этого не произошло, для поставки необходимо добавить в конфиг [app.conf](src/script/app.conf)
в секцию **_dictionaries.yt.tables_** словарь, указав параметры загрузки
 * **_clickhouse_table_** - как будет называться таблица в ClickHouse
 * **_from_** - начиная с какой даты начать отгружать словарь в ClickHouse
 * **_sharding_key_** - по какому ключу будет шардироваться


### Поставка неисторических словарей

По историческим причинам поставкой занимается
[clickphite](https://github.yandex-team.ru/market-infra/market-health/tree/master/clickphite).

Эти словари поставляются в dict схему.

Для того, чтобы добавить новый словарь, нужно:
 1. Добавить по аналогии словарь в
 [clickphite dicts package](https://github.yandex-team.ru/market-infra/market-health/blob/master/clickphite/src/main/java/ru/yandex/market/clickphite/dictionary/dicts)
 2. Выкатить и посмотреть (например на разработческой тачке callisto) по логам
 и в локальном clickhouse (он там на localhost), что все ок
 (при необходимости произвести некоторые действия с ddl по аналогии с liquibase. подробнее к staff:andreevdm)
 3. Создать pull-request и ждать когда команда проверит и tsum-pipeline раскатит.
 4. Глянуть на тестинге clickphite, что все ок в тестовом clickhouse (health-house-testing.market.yandex.net)
 5. После выкатки убедиться health-house.market.yandex.net , иначе спросить дежурного или самому глянуть логи.

Для того, чтобы словарь стал [внешний словарь в ClickHouse](https://clickhouse.yandex/docs/ru/dicts/external_dicts)
нужно так же добавить его в
[конфиг ClickHouse](https://github.yandex-team.ru/market-infra/market-clickhouse-formula/blob/master/health/welder/root/etc/clickhouse-server/dictionary.xml)
создать pull-request и попросить раскатить.

### Поставка данных из market-data-getter
Перед добавлением выгрузки в коде словарей, нужно привезти необходимые файлы в контейнеры:

https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/sandbox-data-getter/marketstat-testing.yaml

https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/sandbox-data-getter/marketstat.yaml

Как тестировать загрузку словаря
================================
Смотри раздел в [integration-test](src/integration-test/README.md)

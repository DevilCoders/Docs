# Как создать счетчик

## Что может считать счётчик

Сумму. Сумма может быть сгруппирована по айди, дням/произвольным отрезкам времени, дополнительным полям и пофильтрована по каким-то ещё полям. Если немного поконтрибьютить, то минимум и максимум.

Если вам нужна медиана или ещё что-то не похожее на сумму в части агрегации, то это не к статисту.

Статист это простые счётчики + кэши. Кэш используется не только по прямому назначению (для ускорения доступа), но так же для фоллбэка в случае, если clickhouse отвечает медленно или недоступен.

## Типы
В statist-е есть 2 типа счётчиков - **default** и **wide**. Это варианты предоставить апи к 2 способам разложения данных по компонентам, когда множество компонент большое и/или меняется, и когда оно фиксированное и достаточно мало чтобы завести на каждый по колонке. Второй случай должен быть эффективней (потому что clickhouse это колоночное хранилище), но первый может быть проще поддерживать.

### Обычный

Значения компонент заранее не определены.

В дефолтном счётчике компоненты в таблице задаются через значение поля **component**, и мы можем считать либо сумму по числовой колонке с именем **total**, либо количество строк.
В конфиге это задаётся через **aggregation-function = count | sum**

Пример конфига с подсчётом строк:
```
autoparts_user {
    type = "default"
    table = "autoparts_stats_event_log_user_counter"
    aggregation-function = count
    filter-fields { //оставшиеся колонки можо использовать для фильтрации
      card_rid = "int64"
      card_type = "string"
      feed_id = "string"
      category_ids = "int64"
    }
}
```

Его таблица, колонки total в ней нет, потому что агрегация делается подсчётом строк:
```
CREATE TABLE autoru_stats.autoparts_stats_event_log_user_counter ON CLUSTER '{cluster}'
(
  day Date, //дискретизация времени только по дню, обязательная колонка 
  id String, //обязательная колонка
  component String, //тоже обязательная
  card_rid UInt32, //дальше поля для фильтрации
  feed_id String,
  card_type String,
  category_ids Array(UInt32)
)
ENGINE = ReplicatedMergeTree('/clickhouse/tables/autoru_stats/autoparts_stats_event_log_user_counter', '{replica}')
PARTITION BY toYYYYMM(day)
ORDER BY (id, component, day) //если не указан PRIMARY KEY, то он равен ключу сортировки, ReplicatedMergeTree не агрегирует данные по ключу, те может быть несколько строк с одинаковыми id-component-day (иначе как бы мы фильтровали по feed_id)
SETTINGS index_granularity = 8192;
```

Её вьюха, group by в ней нет, так как ReplicatedMergeTree таргет-таблицы ничего не агрегирует:
```
CREATE MATERIALIZED VIEW autoru_stats.autoparts_stats_event_log_user_view ON CLUSTER '{cluster}' TO autoru_stats.autoparts_stats_event_log_user_counter
AS
  SELECT day, component, owner_dealer_uid as id, card_rid, feed_id, card_type, category_ids
  FROM autoru_stats.autoparts_stats_event_log;
```

### Широкий

Значения компонент заранее известны и их мало.

В широком счётчике значения по нескольким компонентам хранятся в колонках по названию компонентов, например просмотры офферов с разных платформ будут хранится в колонках ios, android, итд.
Доступные для широкого счетчика агрегации:
- sum(*component_name*)
- uniqStateMerge(*component_name*)

В конфиге это задаётся через **wide-aggregation-function = sum (default) | uniqexactmerge**.

Для агрегации uniqStateMerge у таблицы должен быть движок **ReplicatedAggregatingMergeTree**.

## Наименование

Старайтесь придерживаться шаблона `x_per_y_by_z`, где:
* `x` - описание компонена (в ед. ч.)
* `y` - список полей для фильтрации, начиная (если имеется) с id (в ед. ч.)
* `z` - поле `granularity` из настроек счетчика (`day` или `time`)

Например, если мы считаем типы событий (это компонент) по офферу (это `id
`), с возможностю фильтрации по региону, то название получится `event_type_per_offer_region_by_day`.

Если мы считаем определенное событие (это компонент) по марке (это поле фильтрации) среди всех офферов, то счетчик следует назвать `card_view_per_mark_by_day`.

## Примеры

### Пример счетчика с sum

Здесь в качестве движка таблицы выбран ReplicatedSummingMergeTree, который в фоновом режиме будет суммировать счётчики по компонентам в рамках ключа сортировки (секция ORDER BY).

Пример конфига счётчика:
```
card_view_per_app_sum {
    type = "wide" //широкий счётчик
    table = "card_view_per_app_counter_day_sum" //имя таблицы без имени базы
    wide-aggregation-function = sum
    components = ["desktop", "android", "ios", "mobile"] //имена числовых колонок со значениями по компонентам
    granularity = "day" //кроме id, данные агрегируются по дню, ещё можно было выбрать time, для случая, когда поле с дискретизированным врееменем в таблице называется timestamp (например его округяют до часа), дискретизацией времени занимается mat view
    numeric-id = false //id строковый
}
```
Таблица этого счётчика:
```
CREATE TABLE autoru_public.card_view_per_app_counter_day_sum ON CLUSTER '{cluster}'
(
    day Date,
    id String,

    desktop UInt64,
    android UInt64,
    ios UInt64,
    mobile UInt64
)
    ENGINE = ReplicatedSummingMergeTree('/clickhouse/tables/autoru_public/card_view_per_app_counter_day_sum', '{replica}')
    PARTITION BY toYYYYMM(day) //способ хранения, не связан с группировкой данных 
    ORDER BY (id, day) //ключ сортировки являеется ключом для группировки в ReplicatedSummingMergeTree
    SETTINGS index_granularity = 8192; //гранулярность индекса менеять не надо, 8192 это магическое число
```

Materialized view счётчика (т.е. триггер на вставку в таблицу с сырыми событиями (autoru_public.event), наполняющий таблицу, описанную выше) имеет некоторые важные особенности:

! Описанная во вью группировка применяется только к вставляемым данным, она не читает таргет-таблицу, дальнейшая группировка делается за счёт движка таргет-таблицы

! Имена полей в select и таблице, в которую происходит вставка, должны совпадать

! Ключи группировки (group by) в select и сортировки в таблице (order by) должны совпадать

```
CREATE MATERIALIZED VIEW autoru_public.card_view_per_app_counter_view_day_sum ON CLUSTER '{cluster}' TO autoru_public.card_view_per_app_counter_day_sum
AS
    SELECT
       toDate(`timestamp`) AS day, //дискретизируем таймстамп по дню, granularity
       offer_id as id, //айди в таблице должно называться id
       sum(if(app='DESKTOP', 1, 0)) as desktop,
       sum(if(app='ANDROID', 1, 0)) as android,
       sum(if(app='IOS', 1, 0)) as ios,
       sum(if(app='MOBILE', 1, 0)) as mobile
    FROM autoru_public.event
where app in ('DESKTOP', 'ANDROID', 'IOS', 'MOBILE') and offer_id != '' and event_type == 'CARD_VIEW'
GROUP BY offer_id, day; 

```

### Пример счетчика с uniqStateMerge

Пример конфига счётчика:
```
card_view_per_app_sum {
    type = "wide" //широкий счётчик
    table = "dealer_unique_active_offers" //имя таблицы без имени базы
    wide-aggregation-function = uniqexactmerge
    components = ["autoru_active_counter", "avito_active_counter", "drom_active_counter", "total_active_count"] //имена колонок с промежуточным состоянием
    granularity = "day" //кроме id, данные агрегируются по дню, ещё можно было выбрать time, для случая, когда поле с дискретизированным врееменем в таблице называется timestamp (например его округяют до часа), дискретизацией времени занимается mat view
    numeric-id = true //id числовой
}
```


Таблица этого счётчика:

! Обязательно движок **ReplicatedAggregatingMergeTree**.

```
create table autoru_public.dealer_unique_active_offers ON CLUSTER '{cluster}'
(
    day                 Date,
    id                  UInt64,
    category            String,
    section             String,
    autoru_active_count AggregateFunction(uniqExact(), UInt64),
    avito_active_count  AggregateFunction(uniqExact(), UInt64),
    drom_active_count   AggregateFunction(uniqExact(), UInt64),
    total_active_count  AggregateFunction(uniqExact(), UInt64)
) ENGINE = ReplicatedAggregatingMergeTree('/clickhouse/tables/{shard}/autoru_public.dealer_unique_active_offers', '{replica}') 
order by (day, id, category, section) 
partition by day;
```

Materialized view счётчика (комбинатор If опционален):

```
create materialized view autoru_public.dealer_unique_active_offers_view ON CLUSTER '{cluster}' to autoru_public.dealer_unique_active_offers
as
SELECT day,
       client_id                                                                                    as id,
       category,
       section,
       uniqExactStateIf(card_id, autoru_status == 'ACTIVE')                                         as autoru_active_count,
       uniqExactStateIf(card_id, avito_status == 'ACTIVE')                                          as avito_active_count,
       uniqExactStateIf(card_id, drom_status == 'ACTIVE')                                           as drom_active_count,
       uniqExactStateIf(card_id, autoru_status == 'ACTIVE' or avito_status == 'ACTIVE' or drom_status == 'ACTIVE') as total_active_count
FROM autoru_public.offer_status
group by day, client_id, category, section;
```

## Движки

Самая важная часть, как сделать чтобы счётчик считал то, что нужно. В статисте нужно использовать Replicated* движки.

### ReplicatedMergeTree
из примера дефолтного конфига, вообще не агрегирует нифига. Сам по себе primary key в clickhouse [не требует уникальности](https://groups.google.com/g/clickhouse/c/eUrsP30VtSU/m/p4-pxgdXAgAJ), если этого не требует движок, и используется только для создания индекса. В дефолтном счётчике с режимом count подойдёт только такой движок.

### ReplicatedSummingMergeTree
из примера широкого конфига, суммирует всё что не в ORDER BY, отлично подходит для простых счётчиков (и в дефолтном конфиге с aggregation-function = sum его тоже можно использовать)

### ReplicatedAggregatingMergeTree
когда хочется странного, например хранить максимальное значение по ключу. Пример таблицы для default счётчика с максимальным total-ом:
```
CREATE TABLE my_domain.max_by_id_and_day ON CLUSTER '{cluster}'
(
    day Date,
    id String,
    component String,

    total SimpleAggregateFunction(max,UInt64) //тут нужно указать аггрегирующую функцию, иначе будет бедлам 
)
    ENGINE = ReplicatedAggregatingMergeTree('/clickhouse/tables/my_domain.max_by_id_and_day', '{replica}')
    PARTITION BY toYYYYMM(day) 
    ORDER BY (id, day)
    SETTINGS index_granularity = 8192;
```
Statist будет селектить от неё sum (потому что мы ничего другого пока не поддерживаем, если надо, добавим max), т.е. делать

```
select sum(total) from my_domain.max_by_id_and_day where day = 'x' and id = 'y' and component = 'z' 
```
Поэтому колонки-фильтры в такой таблице сейчас будут бесполезны (если вы не хотите получить сумму максимумов).
И запросы за несколько дней тоже вернут сумму максимумов.
[Альтернативные](https://clickhouse.tech/docs/en/sql-reference/data-types/simpleaggregatefunction/) агрегирующие функции (честно сказать, кроме min там ничего полезного)

### ReplicatedReplacingMergeTree

Хранит строчки, уникальные по ключу сортировки. Можно использовать в default count счётчике чтобы считать уников.
Если вам важно, какая именно строчка выживет при replace-е одинакового ключа (те в ключе не все поля таблицы),
то можно указать поле (типа UInt*, Date или DateTime), по которому будет выбран победитель, например более позднее событие.

Hапример число уникальных офферов по региону и типу машины по информации, в которой эти офферы могут дублироваться:
```
CREATE TABLE autoru_public.distinct_offers_counter_day ON CLUSTER '{cluster}'
(
    day Date,
    id UInt64,
    mark String,
    model String,
    generation_id UInt64,
    offer_id
)
    ENGINE = ReplicatedReplacingMergeTree('/clickhouse/tables/autoru_public/distinct_offers_counter_day', '{replica}')
    PARTITION BY toYYYYMM(day)
    ORDER BY (id, day, mark, model, generation_id, offer_id)
    TTL day + toIntervalMonth(1) //лучше выставлять ттл, если старые данные вам не нужныы
    SETTINGS index_granularity = 8192;
```

```
CREATE MATERIALIZED VIEW autoru_public.distinct_offers_counter_day_view ON CLUSTER '{cluster}' TO autoru_public.distinct_offers_counter_day
AS SELECT
   toDate(`timestamp`) AS day,
   owner_location_federal_subject_id as id,
   card_mark as mark,
   card_model as model,
   card_generation as generation_id,
   offer_id
FROM autoru_public.event
```

```
distinct_offers {
type = "default"
table = "distinct_offers_counter_day"
aggregation-function = count
filter-fields {
  mark = "String"
  model = "String"
  generation_id = "UInt64"
}
numeric-id = true
}
```

## TTL

Как мы уже рассмотрели, mat view это триггер на вставку. Т.е. ttl таблицы с сырыми данными никак не влияет на время жизни данных в таблицах счётчиков. Возможно вы захотите пожалеть кликхаус и поставить на свою таблицу-счётчик ttl.

Делается это так:
```
    ...окончание запроса на создание таблички...
    TTL day + toIntervalMonth(1)
    SETTINGS index_granularity = 8192;
```

Если TTL меньше месяца, то дефолтное партиционирование по месяцу становится бессмысленным. Можно [поставить](https://clickhouse.tech/docs/ru/engines/table-engines/mergetree-family/custom-partitioning-key/) по какому-то энаму, например.

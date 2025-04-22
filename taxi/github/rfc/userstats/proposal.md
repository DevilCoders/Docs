## Что за сервис userstats, как сейчас работает и для чего нужен

Сервис userstats хранит в себе количество поездок пользователей, сохраненное в привязке к идентификаторам: `phone_id`, `yandex_uid`, `device_id`, `card_id`. Кроме того, число поездок хранится в разрезе по тарифам (эконом, комфорт и т.д.) и брендам (ЯТакси, Убер, Янго).

Сервис написан на базе backend-cpp. Счетчики поездок хранятся в mongo-коллекциях `phone_counters`, `yandex_counters`, `device_counters`, `card_counters` в базе `dbuserstats`. Для обновления счетчиков есть ручка `update`, для получения счетчиков - ручка `stats`.

Основной потребитель сервиса - сервис купонов. Некоторые серии промокодов настроены таким образом, что промокод работает только на первые N поездок: например, первые поездки в сервисе вообще - для программы рефералки, или первые поездки в тарифе - для промоутирования тарифа. Другой пример - возможность приглашать друзей по реферальной программе открывается, только если у пользователя есть поездки по карте (для борьбы с фродом). Для максимизации эффективности борьбы с фродом счетчики поездок хранятся сразу по нескольким идентификаторам, а не только, скажем, по `yandex_uid` или `phone_id`.

## Структура хранения данных и ее недостатки

Для хранения счетчиков используются mongo-коллекции с вложенной структурой. Все коллекции `phone_counters`, `yandex_counters`, `device_counters`, `card_counters` идентичны по структуре, поэтому будем смотреть на `phone_counters`, подразумевая все остальные тоже. Пример документа из коллекции:

```json
{
  "_id" : "5d0b7fb1629526419ee8cfad",
  "transactions" : [
    "11a5920aac5616bf82865eeb0866019e",
    "4f09fd29fd345936adb71b923841850d",
    "7d5c55a44bc91e9fb155e5c8d3a0ef81",
    "4c3ab23c1cb72110b3a212aedb8bc1d3",
    "b8b7f489662f2d848f10796f3085ce49",
    "f9041b2c3abb2355a70d1b3d86f9d86c",
    "94fc110635a35b84b4078b80c9b93352",
    "53817d9d9665659799fba17a55abeb4c",
    "0b1cad6b4674364badf31239f9879ebe",
    "7784deb8f0b95657b9fe32cf6d2f2dcd"
  ],
  "tariffs" : {
    "business" : {
      "value" : 10
    },
    "econom" : {
      "value" : 72
    },
    "minivan" : {
      "value" : 1
    },
    "vezeteconom" : {
      "value" : 5
    },
    "vezetstart" : {
      "value" : 3
    },
    "comfortplus" : {
      "value" : 3
    }
  },
  "updated" : "ISODate('2020-04-23T20:03:58.787Z')",
  "created" : "ISODate('2019-06-24T11:16:03.180Z')",
  "brand" : {
    "vezet" : {
      "tariffs" : {
        "vezetstart" : {
          "value" : 3
        }
      },
      "transactions" : [
        "c7a8718dd12b640aa6dbd20fa58447b3",
        "5e13c4b967752e9892c79a152e2947ad",
        "4fa03d3bd605235aba756f0ffc799bdd"
      ]
    }
  }
}
```

Поле `_id` является идентификтором соответствующей сущности (для `phone_counters` - `phone_id`).
Список `transactions` хранит последние 10 идентификаторов заказов. Нужен для защиты от повторных записей для одного и того же `order_id`.

Сами счетчики лежат в полях по путям, которые строятся следующим образом: `property1.value1...propertyN.valueN.value`, то есть, например, количество заказов в бренде Везет в тарифе Старт лежат по пути `brand.vezet.tariffs.vezetstart.value` (и равно 3 в примере документа выше).

Когда вводили сущность "бренд", не стали проводить миграцию старых данных и разделять заказы по брендам, поэтому для части брендов данные общие, задается [конфигом](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/USERSTATS_BRANDS_NO_FIELD_PREFIX?name=brands_no). Так как Давос не запустили, то по факту все бренды смешаны.

### Недостатки текущей структуры

- Отсутствие единообразия: разные бренды хранятся по-разному, и по сути разная гранулярность данных для разных брендов.
- Одинаковые по структуре коллекции - лишние сущности, можно хранить все в одной коллекции. При добавлении нового идентификатора придется новую коллекцию заводить.
- Вложенная структура затрудняет добавление нового разреза в данные + с каждым новым уровнем формат усложняется.
- Непонятно как проводить миграцию данных, если потребуется добавить новый разрез для хранения счетчиков - а именно это и потребовалось, например, [здесь](https://st.yandex-team.ru/TAXIBACKEND-28854).

## Текущее API и его недостатки

### Ручка update

Ручка обновляет информацию по счетчикам. По всей видимости, нужна была раньше, так как STQ-таска написана на питоне, а сервис в backend-cpp. Если переделать сервис на uservices, то можно сделать обработчик STQ внутри сервиса и такая ручка не будет нужна.

Из минусов:
- Детали реализации торчат наружу через API - пользователь передает список счетчиков в виде путей для тарифов, бренд идет отдельным параметром. Так же наружу торчат операции монги (`$inc`) в ручке для обновления счетчиков заказов. Хотя, возможно, это задумывалось, как универсальное API для складывания статистики в монгу.

### Ручка stats

Балковая ручка для запроса статистики, пример запроса:

```json
{
  "brand": "yataxi",
  "bulk_ids": {
    "phone_id": [
      "123",
      "321"
    ],
    "card_id": [
      "1234",
      "12345"
    ]
  },
  "counters": [
    "tariffs.econom"
  ]
}
```

## Предложение по выносу сервиса userstats в uservices

Сервис написан давно на базе репозитория backend-cpp, который более не поддерживается. Для дальнейшего развития сервиса предлагается переписать его на uservices.

### Хранение метрик

Для хранения счетчиков заказов предлагается следующая схема БД в postgres:

```sql
CREATE TYPE identity_type AS ENUM ('phone_id', 'yandex_uid', 'card_id', 'device_id');

CREATE TABLE userstats.orders_counters (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid()
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  identity_type_name identity_type NOT NULL,
  identity_value TEXT NOT NULL,
  counter_value INTEGER NOT NULL,
  counted_from TIMESTAMPTZ NOT NULL,
  counted_to TIMESTAMPTZ NOT NULL,
  tariff TEXT NOT NULL UNIQUE,
  brand TEXT NOT NULL UNIQUE,
  payment_method_type TEXT NOT NULL UNIQUE
);

CREATE UNIQUE INDEX orders_counter_idx_tariff_brand_payment_type
  ON userstats.orders_counter (identity_value, identity_type_name, tariff, brand, payment_method_type)
  INCLUDE (counter_value);
```

При добавлении нового типа идентификатора пользователя, нужно просто расширить тип `identity_type`.

При добавлении нового разреза данных нужно будет сделать следующее:
- Добавить NULLable поле в таблицу `userstats.orders_counters`.
- Создать новый индекс `orders_counter_idx_tariff_brand_payment_type_new_field` (`CONCURRENTLY`), содержащий новое поле.
- Удалить старый индекс `orders_counter_idx_tariff_brand_payment_type`.
- Провести миграцию данных - разделить старые данные в соответствии с новым разрезом. Миграции будет посвящена отдельная часть проработки.
- Сделать новое поле NOT NULL.

### Наполнение данных

Наполняться новое хранилище будет в STQ-обработчике `userstats_order_complete`. Таска будет ставиться из нового процессинга после успешного завершения заказа. В таску передаем id заказа, по которому в обработчике получаем необходимые данные (тариф, бренд и т.д.) и обновляем счетчик в таблице `userstats.orders_counter`.

STQ гарантирует, что одномоменто выполняется одна таска с одним `task_id`, но не защищает от повторных постановок тасок. Например, если какие-то проблемы в процессинге, то, вероятно, могут быть повторно поставлены таски с тем же `order_id`. Для защиты от таких ситуаций можно использовать отдельную таблицу:

```sql
CREATE TABLE userstats.processed_orders (
  id BIGSERIAL PRIMARY KEY,
  order_id TEXT NOT NULL UNIQUE,
  created_at TIMESTAMPTZ NOT NULL
);
```

Таблицу нужно будет периодически чистить, так как заказов много. Можно держать, например, заказы за последние N дней. Это не защитит от повторной постановки задачи спустя большой интервал времени, но, кажется, ошибки при постановке тасок из процессинга должны быть кратковременными, поэтому повторные задачи с тем же `order_id` если и случаются, то на небольшом горизонте времени.

**Важно:** STQ-таску из процессинга надо ставить, только если статус заказа _изменился_ на успешный. Процессинг успешных заказов может запускаться повторно спустя доводльно продолжительное время. Для этого надо ставить таску по событию `handle_complete`.

Примерный запрос для обновления статистики (если заказа еще нет в таблице `userstats.processed_orders`) для одного идентификатора (например, `phone_id`):

```sql
BEGIN TRANSACTION;

INSERT INTO userstats.processed_orders (order_id) VALUES ($1); -- order_id

INSERT INTO userstats.orders_counters
(
  identity_type_id,
  identity_value,
  counter_value,
  counted_from,
  counted_to,
  tariff,
  brand,
  payment_method_type
)
VALUES
(
  $1,         -- identity type
  $2,         -- identity value
  1,          -- initial counter value
  $3,         -- order.proc_created
  $3,         -- order.proc_created
  $4,         -- tariff
  $5,         -- brand
  $6          -- payment_method_type
)
ON CONFLICT DO UPDATE
SET
  counter_value = counter_value + 1,
  counted_from = MIN(counted_from, EXCLUDED.counted_from),
  counted_to = MAX(counted_to, EXCLUDED.counted_to)
COMMIT;
```

Делать ли последовательные запросы для всех идентификаторов в транзакции, либо обновлять их пачкой - зависит от того, будет ли применяться шардирование.

Айдишники для traiff, brand, и т.д. можно доставать из справочников (с их обновлением) до выполнения основной транзакции с обновлением счетчиков.

### Доступ к данным

Данные можно будет получить с помощью ручки:

```yaml
paths:
    /v1/orders:
        post:
            parameters:
              - name: body
                in: body
                required: true
                schema:
                    $ref: '#/definitions/OrdersRequest'
            responses:
                200:
                    description: OK
                    schema:
                        $ref: '#/definitions/OrdersResponse'
                400:
                    description: некорректны входные параметры
                500:
                    description: внутренние ошибки сервиса

definitions:

    OrdersStatsIdentity:
        type: object
        additionalProperties: false
        properties:
            type:
                description: Тип идентификатора.
                type: string
                enum:
                  - phone_id
                  - device_id
                  - card_id
                  - yandex_uid
            value:
                description: Значение идентификатора.
                type: string
        required:
          - type
          - value

    OrdersStatsProperty:
       type: string
       enum:
         - brand
         - payment_method_type
         - tariff

    OrdersStatsPropertyValue:
        type: object
        additionalProperties: false
        properties:
            name:
                $ref: #/definitions/OrdersStatsProperty
            value:
                description: Значение параметра.
                type: string
        required:
          - name
          - value

    OrdersRequest:
        type: object
        additionalProperties: false
        properties:
            identities:
                type: array
                items:
                    $ref: #/definitions/OrdersStatsIdentity
            filters:
                type: array
                description: |-
                    Список фильтров для параметров счетчиков,
                    объединяемых условием "И". Для каждого свойства
                    можно указать не более одного значения.
                items:
                    $ref: #/definitions/OrdersStatsPropertyValue
            group_by:
                type: array
                items:
                    $ref: #/definitions/OrdersStatsProperty
        required:
          - identities
          - filters
          - group_by

    OrderIdentityDataItem:
        type: object
        additionalProperties: false
        properties:
            properties:
                type: array
                items:
                    $ref: #/definitions/OrderStatsPropertyValue
            counter_value:
                type: integer
                min: 0
        required:
          - properties
          - counter_value

    OrderResponseDataItem:
        type: object
        additionalProperties: false
        properties:
            identity:
                $ref: #/definitions/OrdersStatsIdentity
            data:
                type: array
                items:
                    $ref: #/definitions/OrderIdentityDataItem
        required:
          - identity
          - data

    OrdersResponse:
        type: object
        additionalProperies: false
        properties:
            data:
                type: array
                items:
                    $ref: #/definitions/OrderResponseDataItem
        required:
          - data
```

Пример запроса:

```json
{
  "identities": [
    {
      "type": "phone_id",
      "value": "12345"
    },
    {
      "type": "yandex_uid",
      "value": "67890"
    }
  ],
  "filters": [
    {
      "name": "brand",
      "value": "yataxi"
    }
  ],
  "group_by": [
    "payment_method_type",
    "tariff"
  ]
}
```

Пример ответа:

```json
{
  "data": [
    {
      "identity": {
        "type": "phone_id",
        "value": "12345"
      },
      "data": [
        {
          "properties": [
            {
              "name": "payment_method_type",
              "value": "cash"
            },
            {
              "name": "tariff",
              "value": "econom"
            }
          ],
          "counter_value": 5
        },
        {
          "properties": [
            {
              "name": "payment_method_type",
              "value": "card"
            },
            {
              "name": "tariff",
              "value": "econom"
            }
          ],
          "counter_value": 10
        }
      ]
    },
    {
      "identity": {
        "type": "yandex_uid",
        "value": "67890"
      },
      "data": [
        {
          "properties": [
            {
              "name": "payment_method_type",
              "value": "cash"
            },
            {
              "name": "tariff",
              "value": "econom"
            }
          ],
          "counter_value": 5
        },
        {
          "properties": [
            {
              "name": "payment_method_type",
              "value": "card"
            },
            {
              "name": "tariff",
              "value": "econom"
            }
          ],
          "counter_value": 10
        }
      ]
    }
  ]
}
```

Балковость ручки нужна, например, чтобы за один запрос вытащить информацию по нескольким идентификаторам пользователя. Это типичный сценарий использования в сервисе купонов.

## Миграция данных

### Первичная миграция после запуска сервиса

Миграцию историчных данных нужно будет запускать после того, как будет включена запись новых данных через STQ-таску `userstats_order_complete`. STQ-таска обновляет поля `counted_from` и `counted_to`, таким образом поддерживая интервал времени, которому соответствует посчитанная статистика. `counted_from` - время создания первого заказа, учтенного в счетчике, `counted_to` - последнего заказа.

**Важно**: в STQ-таске начинаем учитывать заказы, **_созданные_** после определенного момента времени (задаем конфигом, например), которое лучше выставить с запасом вперед. Это позволит избежать следующей ошибки в подсчетах: заказ, который создан позже, завершается раньше (возможно, например, при мультизаказе).
```
   O1S   O2S   O2F   STQ_LAUNCH   O1F     t
----v-----v-----v---------v--------v------>
```
Здесь включение STQ-таски в указанный на диаграмме момент приведет к тому, что в счетчике будет учтен заказ O1, и выставлено поле `counted_from == O1.created`. При этом заказ O2 не будет учтен в счетчике (так как завершился до включения STQ-таски) и будет проигнорирован при миграции.


Историчные данные можно выгрузить из YT из таблицы `home/taxi/{unstable,testing,production}/replica/mongo/struct/orders_full` кластера `hahn`, в которую реплицируются данные заказов. Данные реплицируются с задержкой, поэтому нужно выждать время после включения сервиса, прежде чем запускать сбор историчных данных.

Необходимые поля:
- id - order_id
- created_proc - время создания заказа
- user_phone_id - phone_id
- device_id - device_id
- payment_tech_main_card_persistent_id - card_id
- user_uid - yandex_uid
- statistics.application - для определения бренда через [конфиг](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/APPLICATION_MAP_BRAND?name=application_map)
- payment_tech_type - payment_method_type
- performer_tariff_class - tariff

Далее для каждого идентификатора (phone_id, yandex_uid, ...) и набора значений для разрезов (brand, tariff, ...) оставляем только те заказы, которые были созданы до `counted_from` соотвествующей записи из таблицы `userstats.orders_counters`. Если записи нет - использовать момент времени включения STQ-таски `userstats_order_complete`. Полученные заказы надо сгруппировать по разрезам и обновить счетчики в таблице `userstats.orders_counters`.

### Миграция после добавления нового идентификатора

Принципиально не отличается от первичной миграции, только не нужно трогать данные для старых идентификаторов.

### Миграция после добавления нового разреза

Как было описано выше, при добавлении нового разреза появляется новый NULLable столбец в таблице `userstats.orders_counters`. Пусть для примера это будет город (столбец `city`), в котором совершена поездка. Новые заказы агрегируются в отдельных записях, в которых заполнено поле "город", однако остались записи, в которых `city IS NULL`. Это те записи, в которых складывалсь информация до появления нового разреза, и они больше не обновляются.

Эти записи с `city IS NULL` надо "распилить" в соответствии с новым разрезом на поездки по городам. Благодаря полям `counted_from` и `counted_to` мы знаем, заказы за какой интервал посчитаны в данной записи. Далее, повторяя процедуру первичной миграции, нужно выгрузить все заказы, отфильтровать нужные, сгруппировать по полному набору разрезов и дописать их в уже актуальные записи с заполняющимся полем "город". Старые записи нужно удалить в той же транзакции, чтобы не было задвоений при чтении.

### Альтернативы реализации

Во время обсуждения проработки предлагались следующие альтернативы по хранилищу данных:

#### Ходить напрямую в YT

Есть кластеры в YT, которые доступны для real-time запросов. Такое, например, используется в ручке `orderhistory` с историей заказов. Однако там не применяется агрегация, а только чтение данных "как есть". Тайминги запросов в YT ~ сотни миллисекунд, что на порядок хуже таймингов всей ручки в текущей реализации userstats. Такие большие тайминги заафектят ручки купонов и расчет цены оффера с промокодом.

#### Использовать Clickhouse

По информации от Группы разработки метрик сейчас Clickhouse используется только в Атласе - для отображения информации (аналитическая задача), опыта использования для продовых задач нет. В будущем есть планы по использованию подобного хранилища, но пока это сильно замедлит разработку + есть риск, что решение не подойдет по производительности.

#### Использовать Clickhouse over YT

Есть возможность запускать "быстрые" запросы над данными в YT. Однако там отсутствует поддержка динамических таблиц:
```
Table //home/taxi/testing/replica/mongo/struct/orders_full is dynamic; dynamic tables are not supported yet (CHYT-57)
```
[Тикету](https://st.yandex-team.ru/CHYT-57) на добавление поддержки - больше двух лет.

### Расширение сервиса для других БЮ (Еда, Лавка)

При возникновении потребности вести аналогичную статистику для сервисов Еды/Лавки можно поднять аналогичные сервисы, которые будут отличаться разрезами данных, схемой БД. Переиспользуемую логику предлагается вынести в библиотеку.

Есть альтернатива с выкаткой одной кодовой базы в разные окружения (т.н. `units`), однако это менее гибкое решение, которое создает связность двух сервисов (одновременные выкатки, единая схема БД). Кроме того, если потребуется добавить кастомное поведение для одного сервиса, то оно попадет в общую кодовую базу и будет отсекаться конструкциями типа `if, switch`.

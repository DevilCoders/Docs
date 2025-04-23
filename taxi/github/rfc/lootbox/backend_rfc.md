# Лутбоксы 🦄


## Базовые понятия

Подарок - промокод, промокод на месяц плюса, скидка в ресторане и тд. Имеет `id` и информацию для описания: тип, id картинки, ...

Лутобокс - множество подарков. Имеет `id` и `gift_ids`.

Серия - сущность, задающая набор лутбоксов, способ выбора следующего лутбокса, условие выпадания лутбокса. Имеет `id`, `lootbox_ids`, `next_lootbox_condition`.

## MVP

Для MVP оставим только безусловные промокоды.
Другие типы подарков не интегрированы в приложение, а MVP хочется сделать максимально дешево.
Эксперимент будет заключаться в сравнении прямого оффера в промоплашке после поездки и/или в поездке: "Скидка 490 рублей на заказ в еде" с лутбоксом с аналогичным подарком.
Такое предложение хотим делать каждую поездку, но не чаще раза в сутки.

В эксперименте будет участвовать 21 миллион пользователей.
Три группы:
* 7 млн с лутбоксом
* 7 млн с прямым оффером
* 7 млн контрольная группа

Ожидаемая конверсия в нажатие, то есть получение промокода, 10%, а в применение 30%.
Соответственно ожидаем выдать `(7 + 7) млн * 0.1  =  1 400 000` промокодов из которых будет применено `1 400 000 * 0.3 = 420 000`.

Если конверсия в заказы с предложенными промокодами будет выше в случае с лутбоксом, то считаем проект успешным.
То есть проверяем гипотезу: красивая анимация конвертирует в заказ лучше, чем просто промокод.
В дальнейшем планируется введение разнообразия подарков, изменение принципа их выдачи.
Например, не каждую поездку, но по несколько штук; не последовательно, а случайно.

### Реализация

* Создаем набор подарков, включающий различные промокоды. Их определяем в конфиге.

* Создаём лутбоксы. По одному для каждого подарка. 
Нужны, чтобы отдавать клиенту один понятный `id` и формировать последовательность лутбоксов. 
Их также определяем в конфиге.
Лутбоксы в MVP можно было бы опустить, так как в них хранится лишь один подарок, но
    * это важный слой абстракции,
    * в противном случае, для добавления произвольного количества подарков в лутбокс понадобится доработка.
 
* Создаём серию, в которую включаем лутбоксы. Задаем их порядок. 
Определяем условие выпадания следующей коробки: каждые X поездок. Серия матчится в эксперименте по `yandex_uid`.


Для подарков и лутбоксов выбрали конфиги, потому что делать удобную админку в MVP дорого, а эксперимент пока не нужен, так как делить пользователей на группы можно в эксперименте серий лутбоксов.

### Схемы экспериментов и конфигов

1. Конфиг с подарками RANDOM_DISTCOUNTS_LOOTBOX_GIFTS_CONFIG

```
default: []
description: Подарки, используемые для лутбоксов: промокоды, др.
tags: [notfallback]
maintainers: [m1eszok]
schema:
    type: object
    properties:
        gifts:
            type: array
                items:
                    $ref: '#/definitions/LootBoxGift'
                x-taxi-cpp-type: std::unordered_set
    required:
        - gifts
    additionalProperties: false

    definitions:
        Promocode:
            type: object
            properties:
                series_id:
                    type: string
            required:
            - series_id
            additionalProperties: false


        LootBoxGift:
            type: object
            properties:
                id:
                    type: string
                type:
                    type: string
                    enum:
                      - promocode
                payload:
                    oneOf:
                    - $ref: '#/definitions/Promocode'
            required:
            - id
            - type
            - payload
            additionalProperties: false
```

2. Конфиг с лутбоксами RANDOM_DISCOUNTS_LOOTBOXES_CONFIG

```
default: []
description: Лутбоксы --- набор подарков.
tags: [notfallback]
maintainers: [m1eszok]
schema:
    type: object
    properties:
        lootboxes:
            type: array
                items:
                    $ref: '#/definitions/LootBox'
                x-taxi-cpp-type: std::unordered_set
    required:
    - lootboxes
    additionalProperties: false

    definitions:
        LootBox:
            type: object
            properties:
                id:
                    type: string
                gift_ids:
                    type: array
                        items:
                            type: string
                type:
                    type: string
                    enum:
                      - box
                      - direct_offer
            required:
            - id
            - gift_ids
            additionalProperties: false
```

3. Эксперимент 3.0 с сериями лутбоксов

```
name: lootbox_series
type: config
description: |
    Серии лутбоксов. Содержат набор лутбоксов, условие выдачи лутбокса.
    В MVP порядок выпадения лутбоксов определяется порядком их записи в серии.

value:
    schema:
        type: object
        properties:
            series:
                type: array
                    items:
                        $ref: '#/definitions/LootBoxSeries'
                    x-taxi-cpp-type: std::unordered_set
        required:
          - series
        additionalProperties: false

definitions:
    NRidesCondition:
        type: object
        properties:
            rides_number:
                type: integer
                minimum: 10
        required:
          - rides_number
        additionalProperties: false



    LootBoxSeries:
        type: object
        properties:
            id:
                type: string
            lootbox_ids:
                type: array
                    items:
                        type: string
            next_lootbox_condition:
                oneOf:
                  - $ref: '#/definitions/NRidesCondition'
        required:
          - id
          - lootbox_ids
          - next_lootbox_condition
        additionalProperties: false
```

### База данных

Для хранения связи пользователя с серией лутбоксов нужно иметь табличку со следующей структурой:
```
{
    'yandex_uid': 'yandex_uid',
    'lootbox_series_id': 'lootbox_series_id', 
    'last_lootbox_update_at': utcnow(),                     # timestamp выдачи последнего лутбокса или совершения действия для получения лутбокса, например, совершение поездки
    'current_user_status': {'rides': 0} или None,           # Состояние пользователя относительно серии. Используется для проверки условия получения лутбокса в серии.
    'lootbox_state': {'last_lootbox_idx': 0} или None,      # Состояние, позволяющее определить, какой лутбокс выдавать следующим. В случае последовательного задания --- индекс в массиве.
    'idempotency_key': 'idempotency_key'        
}
```

Схема для PostgreSQL:
```
CREATE TABLE IF NOT EXISTS random_discounts.user_lootbox_series
(
  yandex_uid                TEXT,
  lootbox_series_id         TEXT,
  last_lootbox_update_at    TIMESTAMPTZ NOT NULL,
  current_user_status       jsonb,
  lootbox_state             jsonb,
  idempotency_key           TEXT,
  PRIMARY KEY(yandex_uid, lootbox_series_id)
);
```

Будут запросы на вставку, обновление и поиск по PRIMARY KEY. 
Дополнительные индексы не нужны.

Количество записей в `user_lootbox_series` есть произведение аудитории на количество серий.
В MVP планируем 2 серии и 14 миллионов пользователей.
Получается, хранить будем порядка 14 миллионов записей.

На запись с запасом заложим 100 байт. 
Итого `0.1 * 14 000 000 = 1 400 000 КБ = 1 400 Мб = 1.4 ГБ`.
Если раскатить на всю аудиторию GO (35 млн MAU): 
`0.1 * 35 000 000 = 3 500 МБ = 3.5 ГБ`.

Также полезным будет хранить историю полученных лутбоксов для пользователя 
```
{
    'yandex_uid': 'yandex_uid',
    'lootbox_series_id': 'lootbox_series_id',
    'lootbox_ids': ['lootbox_id'],
    'idempotency_key': 'idempotency_key'        
}
```

Схема для PostgreSQL:
```
CREATE TABLE IF NOT EXISTS random_discounts.user_lootbox_history
(
  yandex_uid                TEXT,
  lootbox_series_id         TEXT,
  lootbox_ids               ARRAY[]::TEXT[] NOT NULL,
  PRIMARY KEY(yandex_uid, lootbox_series_id)
);
```
Будут запросы на вставку, обновление и поиск по PRIMARY KEY. 
Дополнительные индексы не нужны.

Тут также будет до 14 миллионов записей, и также положим по 100 байт на штуку.
Тогда обе базы для MVP займут порядка `2.8 ГБ`, а при полной раскатке - `7 ГБ`.

Так как поля `current_user_status` и `lootbox_state` имеют произвольную структуру, хочется использовать нереляционную mongodb.
Хотя в новых версиях postgresql тоже можно записывать json поля: [ссылка](https://stackoverflow.com/a/45150668).
Кроме того, в сервисе `random-discounts`, в который добавляем всю логику, уже есть PostgreSQL база, в которую можно добавить несколько табличек.
Поэтому в итоге остановились на варианте с PostgreSQL.

### Пользовательский флоу

В расчётах rps полагаемся на то, что MAU GO порядка 35 млн, а аудитория MVP порядка 21 млн, из них 14 миллионов --- аудитория с лутбоксами.
Вся аудитория GO совершает 7.7 млн поездок в день.
14 млн из выборки примерно 2.26 млн.

* Пользователь заказывает такси

* При вызовах totw вызывается `/4.0/lootbox/v1/fetch_state`, которая проверяет, будет ли в этой поездке пользователю выдан лутбокс. 
При выполнении условия, то есть `{'rides': X}` и `now() - last_lootbox_update_at  > Y`, отдаем `LootboxAction` с id следующего лутбокса: [RFC клиентов](https://a.yandex-team.ru/arcadia/taxi/github/rfc/lootbox/promo_block_lootbox_action.md?from_pr=2647546&rev=users%2Fa-tumanov%2FTAXIMOBILEDEV-1270%2Flootboxes).
Пиковая дневная нагрузка на totw - 6k rps, значит, ожидаемая нагрузка на ручку лутбоксов - до `6 000 * 2.26 / 7.7 = 1761` rps.

* По нажатию на промоплашку открывается экран с закрытым лутбоксом и кнопкой "Забрать всё".
По нажатию на нее, вызываем ручку `/4.0/lootbox/v1/activate`, которая повторно проверяет доступность лутбокса, идемпотентно обновляет информацию в базе и отдает содержимое лутбокса. 
В случае ошибки ручка отвечает 404: [RFC клиентов](https://a.yandex-team.ru/arcadia/taxi/github/rfc/lootbox/lootbox_activate.md?from_pr=2647546&rev=users%2Fa-tumanov%2FTAXIMOBILEDEV-1270%2Flootboxes).
Пиковая дневная нагрузка на `ordercommit` 170 rps.
Предполагаемая конверсия в нажатие - 10%, поэтому ожидаемая нагрузка на ручку лутбоксов - до `170 * 2.26 / 7.7 * 0.2 = 10` rps.

* В конце поездки для пользователей, попадающих под эксперимент, ставим stq, которая обновляет его статус относительно серии лутбоксов: обновляет количество поездок после таймстемпа активации предыдущего лутбокса.
Для получения количества поездок во временном полуинтервале используем ручку [`/v1/recent-orders
`](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/user-statistics/api/api/#v1recent-orders).

Пиковая дневная нагрузка на `ordercommit` 170 rps.
Нагрузка на stq лутбоксов `170 * 2.26 / 7.7 = 50` rps.

### Микросервис

Сервис `random-discounts` выбрали как самый релевантный.
Сейчас он в конфигурации `x2nano` (суммарно 2 ядра, 8 Гб ОЗУ) с медианной пиковой дневной нагрузкой 30 rps.
Сейчас нагрузка на CPU порядка 9%, RAM 33%.
Нагрузка увеличится на 1820 rps, что потребует изменения конфигурации сервиса.
Учитывая увеличение количества запросов в 60 раз, разумным кажется рассмотреть конфигурации `x3micro` с добавлением подов и RAM при необходимости: 
3 дц x 3 пода в конфигурации 2x8 -> 18x72.  



### Cхемы ручек

* `/4.0/lootbox/v1/fetch_state`

```
openapi: 3.0.0
info:
    description: Yandex Taxi random-discounts Service
    title: Yandex Taxi random-discounts Service
    version: '1.0'

# Not used in codegen
servers:
  - url: random-discounts.taxi.yandex.net
    description: production

x-taxi-middlewares:
    tvm: true


x-taxi-client-qos:
    taxi-config: RANDOM_DISCOUNTS_CLIENT_QOS

paths:
    /4.0/lootbox/v1/fetch_state:
        get:
            x-taxi-middlewares:
                api-4.0: true
            parameters:
              - in: header
                name: X-Idempotency-Token
                description: токен, генерируемый клиентом, для идемпотентности запроса
                type: string
                required: true
            description: |
                Проверяет состояние пользователя относительно серии лутбоксов.
            responses:
                '200':
                    description: OK
                    schema:
                        $ref: '#/definitions/LootBoxUpdateStateResponse'
                '400':
                    description: Пользователь не сматчился в эксперименте
                    schema:
                        $ref: '#/definitions/definitions/UserError'

definitions:
    LootBoxUpdateStateResponse:
        type: object
        additionalProperties: false
        properties:
            lootbox_id:
                type: string
                description: Идентификатор лутбокса, который будет выдан в данной поездке.
        required:
          - lootbox_id

    UserError:
        type: object
        additionalProperties: false
        properties:
            message:
                type: string
                description: сообщение об ошибке
                example: "invalid or missing parameters"
            code:
                description: код ошибки
                type: string
        required:
          - message
```

* `/4.0/lootbox/v1/activate`

```
paths:
    /4.0/lootbox/v1/activate:
        post:
            x-taxi-middlewares:
                api-4.0: true
            parameters:
              - in: header
                name: X-Idempotency-Token
                description: токен, генерируемый клиентом, для идемпотентности запроса
                type: string
                required: true
            description: |
                Проверяет выполнение условий выдачи лутбокса, возвращает всю информацию, необходимую для его отображения. 
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            properties:
                                lootbox_id:
                                    type: string
                                    description: Идентификатор лутбокса, который будет выдан в данной поездке.
                            required:
                            - lootbox_id

            responses:
                '200':
                    description: OK
                    schema:
                        $ref: '#/definitions/LootBoxActivateResponse'
                '404':
                    description: |
                        Условия для получения лутбокса пользователем не выполнены
                        или передан непраивльный id лутбокса
                    schema:
                        $ref: '#/definitions/UserError'

definitions:
    Title:
        type: object
        additionalProperties: false
        properties:
            items:
                $ref: '#/definitions/Items'
        required:
          - items
            

    Separator:
        type: object
        additionalProperties: false
        properties:
            items:
                $ref: '#/definitions/Items'
        required:
          - items

    Gifts:
        type: object
        additionalProperties: false
        properties:
            title:
                $ref: '#/definitions/Title'
            subtitle:
                $ref: '#/definitions/Title'
            lead_icon_tag:
                type: string
            lootbox_icon_tag:
                type: string
            action:
                $ref: '#/definitions/Title'
        required:
          - title
          - subtitle
          - lead_icon_tag
          - lootbox_icon_tag
          - action

    LootBoxActivateResponse:
        type: object
        additionalProperties: false
        properties:
            title:
                $ref: '#/definitions/Title'
            separator:
                $ref: '#/definitions/Separator'
            gifts:
                $ref: '#/definitions/Gifts'
            take_all_button:
                $ref: '#/definitions/Button'
        required:
          - service
          - separator
          - gifts
          - take_all_button

        required:
          - lootbox_id

    UserError:
        type: object
        additionalProperties: false
        properties:
            message:
                type: string
                description: сообщение об ошибке
                example: "invalid or missing parameters"
            code:
                description: код ошибки
                type: string
        required:
          - message
```


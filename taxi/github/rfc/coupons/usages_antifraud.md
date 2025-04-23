# Улучшаем антифрод проверки на основе данных об использовании промокодов

## Проблема

В настоящий момент проверки лимитов использования промокодов производятся на
основе коллекции [dbtaxi.promocode_usages2](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Mongo%20collections/taxi/promocode_usages2/).
В этой коллекции ведется учет использований промокодов, но только по `phone_id`
пользователя.

Пример документа из коллекции:

```json
{
  "_id": "ObjectId(5f4f68c0a7bad42a5cad8507)",
  "code": "devcrab200",
  "phone_id": "ObjectId(5d0b7fb1629526419ee8cfad)",
  "series_id": "devcrab200",
  "rides": 3,
  "updated_at": "ISODate(2021-01-20T16:34:51.558Z)",
  "usages": [
    {
      "reserve": "cb0408b226e6303284604dc6f2479664",
      "cost_usage": 169
    },
    {
      "reserve": "24232a070ab557a28167fe8fbadb1c81",
      "idempotency_tokens": [
        "HjP9uosQya3Dcnds2XYk"
      ],
      "cost_usage": 200
    },
    {
      "reserve": "c1dad10d543561398a9ae528c060c3f9",
      "idempotency_tokens": [
        "KsXlGSWY5Mmel72Q3xtI"
      ],
      "cancel_tokens": [
        "KsXlGSWY5Mmel72Q3xtI"
      ]
    },
    {
      "reserve": "839137e0dc413c81b25f7deeaef6be87",
      "idempotency_tokens": [
        "H3zfsb0ZQHNDZJ9Xh1ne"
      ],
      "cost_usage": 200
    }
  ],
  "value": 200,
  "cost_usage": 569
}
```

Фродеры умеют менять `phone_id`, что позволяет им повторно использовать
неуникальные промокоды. Уникальные промокоды не подвержены такой уязвимости,
так как привязываются к конкретному `phone_id` после первого использования.

## Предложение от группы антифрода по уменьшению количества фрода

Нужно вести учет использований не только по `phone_id`, но и по другим
айдишникам пользователя: `yandex_uid`, `device_id`, чтобы при смене одного
айдишника мы не думали, что пришел новый пользователь, и не обнуляли его
использования промокода.

## Реализация

Предлагается в документах коллекции `dbtaxi.promocode_usages2` дополнительно
хранить остальные айдишники пользователя `yandex_uid` и `device_id`:

```json
{
  "_id": "ObjectId(5f4f68c0a7bad42a5cad8507)",
  "code": "devcrab200",
  "phone_id": "ObjectId(5d0b7fb1629526419ee8cfad)",
  "device_id": "1e50abaa3e95bf8542fb5d0c783a8feb",
  "yandex_uid": "4032745524",
  "series_id": "devcrab200",
  "rides": 3,
  "updated_at": "ISODate(2021-01-20T16:34:51.558Z)",
  "usages": "[...]",
  "value": 200,
  "cost_usage": 569
}

```

Также нужно будет добавить уникальные индексы, аналогичные
`series_id_1_code_1_phone_id_1`, которые будут гарантировать, что учет каждого
айдишника внутри промокода и серии производится не более чем в одном документе
коллекции.

Особенности индексов в mongo не позволят сделать это напрямую:

```shell
db.promocode_usages2.createIndex(
  {
    series_id: 1,
    code: 1,
    yandex_uid: 1
  },
  {
    unique: 1
  }
)
```

т.к. mongo считает, что разные документы с отсутствующим (или равным `null`)
полем нарушают уникальность индекса (в отличие, например, от postgres).

Это ограничение помогут обойти [Partial
Indexes](https://docs.mongodb.com/manual/core/index-partial/#partial-index-with-unique-constraints).
Не будем включать в новые индексы старые документы, где поля `yandex_uid` и
`device_id` не заполняются:

```shell
db.promocode_usages2.createIndex(
  {
    series_id: 1,
    code: 1,
    yandex_uid: 1
  },
  {
    unique: 1,
    partialFilterExpression:
    {
      yandex_uid: { $exists: true }
    }
  }
)
db.promocode_usages2.createIndex(
  {
    series_id: 1,
    code: 1,
    device_id: 1
  },
  {
    unique: 1,
    partialFilterExpression:
    {
      device_id: { $exists: true }
    }
  }
)
```

С новыми полями `yandex_uid` и `device_id` и описанными индексами при попытке
вставки документа с существующими айдишниками `phone_id`, `yandex_uid` или
`device_id` (в рамках серии и кода) будет возникать ошибка из-за
UniqueConstraint. Это будет означать, что уже есть документ, в котором ведется
учет использования промокодов для какого-то из этих айдишников. Сам документ
можно будет найти подобным запросом:

```shell
db.promocode_usages2.find(
  {
    series: "code",
    code: "code",
    $or: [
      {
        phone_id: ObjectId("5d0b7fb1629526419ee8cfad")
      },
      {
        yandex_uid: "4032745524"
      },
      {
        device_id: "1e50abaa3e95bf8542fb5d0c783a8feb"
      }
    ]
  }
)
```

Таким образом, новый счетчик использований промокода будет заводиться только
для тех айдишников, которые в рамках серии и кода встречаются впервые. В данном
случае невозможно (с текущим набором данных) отличить настоящего нового
пользователя от фродера, который сменил все айдишники сразу.

## Доработки

### Создать новые индексы

Создать Partial Indexes `series_id_1_code_1_yandex_uid_1`,
`series_id_1_code_1_device_id_1` в коллекции `dbtaxi.promocode_usages2`.

### Пробрасывать нужные айдишники в STQ-таску finish_coupon

Сейчас приходят `phone_id` и `yandex_uid`, но не `device_id`. Нужно доставать в
процессинге этот идентификатор тоже и передавать в STQ-таску.

### Доработать код сервиса coupons

Сделать доработки, описанные в части про реализацию:
- создавать новые документы с набором айдишников
- находить правильным запросом документ с подсчетом использований при проверке
  лимитов

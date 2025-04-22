# Построение офферов

## Офферы

### Оффер `standart_offer`

Представляет базовую реализацию оффера с поминутной оплатной.

### Оффер `pack_offer_builder`

Представляет пакетный тариф с предоплаченными минутами и километражом.

### Оффер `fix_point`

### Оффер `standard_with_discount_area`

Представляет расширенную реализацию оффера `standart_offer` с дополнительными полями для скидок в определенной зоне.

#### Способы построения оффера:

* Пользователь указал точку Б. Расчёт скидки будет происходить с учётом указанной точки.
* Точка Б отсутсвует. В этом случае построится несколько офферов (точки Б будут взяты из `suggest-а`).

## Билдеры

### Билдер `standard_with_discount_area`

Билдер для построения оффера со скидкой. В админке задаётся как `Action` с типом 
`standard_with_discount_area`. 

Конфигурация билдера:

* `base_offer_builder` &mdash; название базового конструктора стандартного оффера (обязательное поле).

* `discount_model` &mdash; название модели для вычисления скидки (необязательное поле).

## Ручки

### Ручка `/api/yandex/offers/standard_with_discount_area/create`

Отвечает за построение оффера со скидкой по уже построенному стандартному офферу.

#### Get параметры

* `base_offer_id` &mdash; id стандартного оффера для построения оффера со скидкой. Обязательное поле.
* `user_destination` &mdash; координаты точки Б, задаваемые пользователем. Необязательное поле.
* `destination_name` &mdash; название точки Б. Необязательное поле.

#### JSON BODY

Отсутствует.

#### Ответ ручки

В ответе возвращается поля похожие на поля стандартного оффера с некоторыми модификациями:
* `finish_area` &mdash; область завершения поездки.
* `finish` &mdash; точка Б (пользовательская или из `suggest-а`).
* `discount` &mdash; скидка, которую насчитала модель.
* `type` &mdash; `standard_with_discount_area_offer`.
* `offer_id` &mdash; id оффера со скидкой (не стандартного!).

##### Примеры запросов

Запрос:

```(bash)
curl 'https://testing.carsharing.yandex.net/api/yandex/offers/standard_with_discount_area/create?base_offer_id=2d0012d5-a0f843a8-dfb7c008-b1eb45d7&user_destination=27.423317+53.912437&destination_name=katyashome' -X GET -H 'Authorization: OAuth XXX'
```

Ответ:

```
{
  "offers": [
    {
      "cashback": {
        "parts": []
      },
      "name": "Нищеброд _",
      "finish_area": "27.41690621 53.90866091 27.42972779 53.90866091 27.42972779 53.91621309 27.41690621 53.91621309 27.41690621 53.90866091 ",
      "subname": "In Rainbows",
      "price_constructor_id": "cheap_base_offer_builder",
      "device_id": "",
      "finish": "27.423317 53.912437",
      "group_name": "",
      "from_scanner": false,
      "short_name": "Min",
      "visual": {
        "offer_visual_type": "",
        "bottom_color": "#FFBF00",
        "top_color": "#003366"
      },
      "agreement": "act_default",
      "is_plus_user": true,
      "finish_name": "katyashome",
      "short_description": [
        "Ожидание — 3 ₽/мин",
        "12 мин бесплатного ожидания"
      ],
      "localizations": {
        "custom_act": "act_default"
      },
      "constructor_id": "cheap_base_offer_builder",
      "parent_id": "",
      "offer_id": "a6eb8dc3-1b7cb361-bbfb386e-dc2050ea",
      "credit_card": "card-x55a40927ca8278e84324d7c0",
      "debt": {
        "threshold": 102400
      },
      "wallets": [
        {
          "selected": true,
          "id": "card"
        }
      ],
      "type": "standard_with_discount_area",
      "detailed_description": "",
      "behaviour_constructor_id": "cheap_base_offer_builder",
      "discount": 0,
      "prices": {
        "parking_discounted": 300,
        "parking": 300,
        "discount": {
          "discount": 0,
          "details": [],
          "id": ""
        },
        "riding_discounted": 500,
        "km": 0,
        "use_deposit": true,
        "riding": 500,
        "insurance_type": "standart",
        "deposit": 27182,
        "free_reservation": 720,
        "km_discounted": 0
      },
      "is_corp_session": false,
      "deadline": 1635527112
    }
  ]
}
```

## Корректоры

### Корректор `offer_corrector_price_model`

// Примечание: если модель будет возвращать значение скидки < 0, то скидка будет увеличена до 0. Если 
значение скидки будет > 1, то скидка будет уменьшена до 1.

#### Параметры

* `dry_run` &mdash; флаг режима dry-run. В этом случае корректор не модифицирует оффер (за исключением некоторых факторов, например `MatrixNet`) и нотификации оффера, а лишь записывает событие `OfferCorrectorPriceModelResult` в лог бекенда.

### Корректор `saturn_model_offer_corrector`

Корректор расширяет базовый корректор [`offer_corrector_price_model`](#korrektor). Он выполняет расчет долгового скоринга и кладет результат в факторы `SaturnOfferScore` и `SaturnOfferScoreRaw`. Далее уже на измененном векторе факторов запускаются оставшиеся модели.

#### GVars

* `offers.saturn_model_offer_corrector.default_threshold` &mdash; значение порога по умолчанию. Если не указано, то `0.9`. Работает только для корректоров без модели `saturn_amount_model`.
* `offers.saturn_model_offer_corrector.enabled` &mdash; включает выполнение корректора. По умолчанию `true`, используется для выключения корректора в случае проблем с Saturn API.
* `offers.saturn_model_offer_corrector.service` &mdash; указывает название сервиса, которое будет отправлено в Saturn API. По умолчанию `drive`.

#### Параметры

* `saturn_amount_model` &mdash; название модели для расчета `amount` для Saturn API. Если не указан, то используется по умолчанию:
  * Для [`standart_offer`](#offer) &mdash; `DestinationDuration * Price / 60.0`, если `DestinationScore` >= `GVars("offers.saturn_model_offer_corrector.default_threshold")`.
  * Для [`pack_offer_builder`](#offer1) (+ остальные) &mdash; `PackPrice`.

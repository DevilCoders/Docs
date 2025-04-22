# Дополнительные услуги

## Получение списка доступных услуг

Для получения используется ручка `/user_app/sessions/current`.

В ответе приходит поле `additional_service_offers` со списком доступных услуг.

{% cut "Пример ответа" %}

```json
{
  "additional_service_offers": [
    {
      "name": "Шиномонтаж",
      "title": "Отдать на шиномонтаж",
      "subtitle": "Пора менять резину",
      "order_button_text": "Записаться",
      "behaviour_constructor_id": "tyre_fitting_offer_builder",
      "offer_id": "a876c6cc-9c6d-47f0-b8e6-0751bc6ecf80",
      "deadline": 1654170968,
      "available_times": [
        {
          "ts": 1654170968
        }
      ],
      "order_fields": [
        {
          "type": "scheduled_at",  // для поля "scheduled_at"
          "title": "Когда забрать машину",
          "subtitle": "После 11"
        },
        {
          "type": "delivery_location",  // для полей "delivery_location" и "delivery_location_name"
          "title": "Куда вернуть машину",
          "same_location": "Туда где взяли"
        },
        {
          "type": "details",
          "title": "Про процесс",
          "subtitle": "Как все будет проходить"
        }
      ]
    }
  ]
}
```

{% endcut %}

## Получение оффера дополнительной услуги

Для получения используется ручка `/api/yandex/offers/create` со следующими `GET` параметрами:

* `car_id` или `car_number`
* `offer_name` &mdash; имеет значение поля `behaviour_constructor_id`.
* `forced_offer_name` &mdash; имеет значение поля `behaviour_constructor_id`.

А также следующим контентом:

```json
{
  "variables": {
    "scheduled_at": 1654170968,
    "delivery_location": [37.61514469, 55.75025475],
    "delivery_location_name": "Кремль"
  }
}
```

{% cut "Пример ответа" %}

```json
{
  "offers": [
    {
      "name": "Шиномонтаж",
      "title": "Отдать на шиномонтаж",
      "subtitle": "Пора менять резину",
      "order_button_text": "Записаться",
      "behaviour_constructor_id": "tyre_fitting_offer_builder",
      "offer_id": "a876c6cc-9c6d-47f0-b8e6-0751bc6ecf80",
      "deadline": 1654170968,
      "available_times": [
        {
          "ts": 1654170968
        }
      ],
      "scheduled_at": 1654170968,
      "delivery_location": [37.61514469, 55.75025475],
      "delivery_location_name": "Кремль",
      "order_fields": [
        {
          "type": "scheduled_at",  // для поля "scheduled_at"
          "title": "Когда забрать машину",
          "subtitle": "После 11"
        },
        {
          "type": "delivery_location",  // для полей "delivery_location" и "delivery_location_name"
          "title": "Куда вернуть машину",
          "same_location": "Туда где взяли"
        },
        {
          "type": "details",
          "title": "Про процесс",
          "subtitle": "Как все будет проходить"
        }
      ]
    }
  ]
}
```

{% endcut %}

## Заказ дополнительной услуги

Для заказа используется ручка `/api/yandex/offers/book` со следующим контентом:

```json
{
  "offer_id": "e208fc15-2708-506c-3634-647fd256f72a"
}
```

## Получения текущего списка услуг

Для получения текущего списка активных услуг нужно использовать ручку `/user_app/sessions/current` с `GET` параметром `multi_sessions=true`.

{% cut "Пример ответа" %}

```json
{
  "additional_service_sessions": [
    {
      "session": {
        "specials": {
          "price_constructor_id": "tyre_fitting_offer_builder",
          "parent_session_id": "1a0a6ac6-10b4-79fb-5a09-d957f860e72b", // ID сессии, для которой оказывается услуга.
          "session_tag_id": "661b213c-8fd6-4a31-ad63-bef02d1bd3c0",  // ID тега.
          "delivery_location": [
            37.61514469,
            55.75025475
          ],
          "session_id": "e208fc15-2708-506c-3634-647fd256f72a",
          "scheduled_at": 1654279797,
          "delivery_location_name": "Some street",
          "available_times": [
            {
              "ts": 1654188616
            },
            {
              "ts": 1654188617
            }
          ],
          "deadline": 1654188856,
          "order_button_text": "Записаться",
          "order_fields": [
            {
              "type": "scheduled_at",  // для поля "scheduled_at"
              "title": "Когда забрать машину",
              "subtitle": "После 11"
            },
            {
              "type": "delivery_location",  // для полей "delivery_location" и "delivery_location_name"
              "title": "Куда вернуть машину",
              "same_location": "Туда где взяли"
            },
            {
              "type": "details",
              "title": "Про процесс",
              "subtitle": "Как все будет проходить"
            }
          ]
        }
      }
    }
  ]
}
```

{% endcut %}

## Изменение дополнительной услуги

Для изменения заказанной услуги используется ручка `/api/yandex/user/tag/update` со следующим контентом:

```json
{
  "tag_id": "661b213c-8fd6-4a31-ad63-bef02d1bd3c0",
  "scheduled_at": 1654279797,
  "delivery_location": [37.61514469, 55.75025475],
  "delivery_location_name": "Some street"
}
```

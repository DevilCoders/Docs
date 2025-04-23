## Бизнесовая задача

Отвечает за информацию об оценках: тексты и типы причин оценок.

## Архитектура

### API

Ручка `GET /v1/low_rating_reason`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
  "low_rating_reason": [
    {
      "label": "Водитель опоздал",
      "name": "driverlate"
    }
  ]
}
```

Ручка `GET /v1/feedback_badges`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
  "feedback_badges": [
    {
      "label": "Запах в машине",
      "name": "bad_smell_4"
    },
  ],
  "feedback_rating_mapping": [
    {
      "badges": [
        "bad_driving_1",
        "rude_driver_1",
        "bad_smell_1",
        "wrong_car_number_1",
        "car_condition_1",
        "no_change_1"
      ],
      "choice_title": "Что вас разочаровало?",
      "rating": 1
    },
  ]
}
```


### v1/low_rating_reasons
Достает причины низкой оценки водителю
Это читается из базы feedback_choices и сверху фильтруется по nearest zone заказа. Если будет кеш
на стороне api-proxy, эту ручку можно дергать один раз.
Еще есть ручка choices в сервисе фидбека, но поход в нее выключен конфигом USE_FEEDBACK_RETRIEVE_CHOICES_HANDLER.
#### Fallback
Ничего, не показываем этот выбор.

### v1/feedback_badges
Достает тексты и типы причин оценки, и для хороших и для плохих оценок
Читается из конфига FEEDBACK_BADGES_MAPPING и фильтруется по классу и типу оплаты. Тоже не нужно в каждом запросе.
Тут же передается и маппинг возможных причин по оценкам.
#### Fallback
Ничего, не показываем этот выбор.

### Технические детали и ограничения
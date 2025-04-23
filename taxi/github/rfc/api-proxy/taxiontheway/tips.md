## Бизнесовая задача

Берет на себя логику чаевых.
Возможно, и для оплаты пригодится, в частности, в проекте с чаевыми по корпоплате.

## Архитектура

### API

Ручка `GET /v1/order_tips`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
  "tips": {
    "available": false,
    "decimal_value": "0",
    "type": "percent",
    "value": 0.0
  }
}
```

Ручка `GET /v1/autoreorder`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
  "tips_suggestions": {
    "variants": [
      {
        "choices": [
          {
            "decimal_value": "22",
            "type": "flat",
            "value": 22.0
          }
        ],
        "customize_options": {
          "decimal_digits": 0,
          "manual_entry_allowed": true,
          "max_value": "1502",
          "min_value": "9"
        },
        "match": {
          "max_rating": 5,
          "min_rating": 4
        }
      }
    ]
  },
}
```


### v1/order_tips
Достает чаевые из ордерпрока. Позже можно начать хранить чаевые в сервисе.
Текущий код можно посмотреть в common/orderkit/src/models/order.cpp/BuildDataTipsInfo и protocol/lib/src/views/taxiontheway.cpp/BuildResponse4Tips
#### Fallback
Ничего, не показываем выбранные чаевые.

### v1/tips_suggestions
Значения чаевых на выбор.
BuildResponse4TipsSuggestions и BuildResponse4TipsVariants. Не забыть забрать логику из GetTipsChoices, ее еще Тигран придумывал.
#### Fallback
Ничего, не предлагаем суммы чаевых.

### Технические детали и ограничения
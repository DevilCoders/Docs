# Резолвер resolveGoOrderHistoryItem

Возвращает список экспресс-заказов пользователя

## Параметры

Обязательный параметр `orderId`

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `orderId` | number | номер заказа пользователя | 1 | - | - |

## Пример запроса

```shell script
curl --request POST \
  --url 'https://<FAPI_HOST>/api/v1?name=resolveGoOrderHistoryItem' \
  --header 'Content-Type: application/json' \
  --data '{
    "params": [
      {
        "orderId": 32773651
      }
  ]
}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveGoOrderHistoryItem",
      "result": {
        "order": {
          "meta_info": null,
          "legal_entities": [
            {
              "additional_properties": [
                {
                  "value": "ООО OOO « Моя попытка номер ДВА»",
                  "title": "Наименование"
                },
                {
                  "value": "1107746275906",
                  "title": "ОГРН"
                },
                {
                  "value": "г.Москва, ул.Енисейская, 11",
                  "title": "Адрес"
                },
                {
                  "value": "Пн-Пт: 10:00-22:00, Сб-Вс: 10:00-16:00",
                  "title": "Часы работы"
                }
              ],
              "title": "Продавец",
              "type": "shop"
            },
            {
              "additional_properties": [
                {
                  "value": "ООО ЯНДЕКС",
                  "title": "Наименование"
                },
                {
                  "value": "1167746491395",
                  "title": "ОГРН"
                },
                {
                  "value": "119021, Россия, г. Москва, ул. Льва Толстого, д. 16",
                  "title": "Адрес"
                },
                {
                  "value": "с 9:00 до 21:00",
                  "title": "Часы работы"
                }
              ],
              "type": "delivery_service",
              "title": "Доставка"
            }
          ],
          "destinations": [
            {
              "short_text": "улица Льва Толстого, 19",
              "point": null
            }
          ],
          "calculation": {
            "discount": "0,00 $SIGN$$CURRENCY$",
            "final_cost": "10000,00 $SIGN$$CURRENCY$",
            "currency_code": "RUB",
            "addends": [
              {
                "name": "Телевизор Samsung UE24H4080 24\"",
                "count": 1,
                "cost": "10000,00 $SIGN$$CURRENCY$",
                "modifiers": []
              }
            ],
            "refund": "0,00 $SIGN$$CURRENCY$"
          },
          "status": "processing",
          "contact": null,
          "created_at": "2021-07-02T08:59:08.778Z",
          "title": "Яндекс.Маркет",
          "service": "market",
          "order_id": 32773651
        }
      }
    }
  ],
  "collections": {}
}
```

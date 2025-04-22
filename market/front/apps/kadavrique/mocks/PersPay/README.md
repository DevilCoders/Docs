# PersPay

## Swagger оригинального бекенда

https://pers-pay.tst.vs.market.yandex.net/swagger-ui.html

## Примеры моков

### Платежные предложения (методы и стейт)
В схему по ключу `paymentOffer` кладём массив объектов, по микроформату https://github.yandex-team.ru/market/microformats/tree/master/paymentOffer

Не указанные поля догенерятся фейкером.
```json
{
    "schema": {
        "paymentOffer": [{
            "amount": 1050,
            "entityId": "1111",
            "entityType": "MODEL_GRADE",
            "payerId": "222",
            "payerType": "VENDOR",
            "userId": "333",
            "userType": "UID"
        }, {
            "amount": 5010,
            "entityId": "1112",
            "entityType": "MODEL_GRADE",
            "payerId": "222",
            "payerType": "VENDOR",
            "userId": "444",
            "userType": "UID"
        }]
  }
}
```

#### Метод getPaymentOffersByModelsAndUser

Отфильтровывает все `paymentOffer` по юзеру (`userId`, `userType`), айди товара (`entityId`) и типу сущности `entityType="MODEL_GRADE"`.

```json

{
    "data": [{
        "amount": 1050,
        "entityId": "1111",
        "entityType": "MODEL_GRADE",
        "payerId": "222",
        "payerType": "VENDOR",
        "userId": "333",
        "userType": "UID"
    }]
}
```


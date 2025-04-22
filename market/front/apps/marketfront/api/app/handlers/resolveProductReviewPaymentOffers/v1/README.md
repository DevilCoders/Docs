# Резолвер resolveProductReviewPaymentOffers

Возвращает общанный кэшбек для указанных товаров для текущего авторизованного пользователя.

Данные в ответе резолвера нормализованы.

## Параметры

Обязательный параметр _productIds_.

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `productIds` | number[] | ProductId | Идентификаторы товаров с обещанным кэшбеком за отзыв для текущего авторизованного пользователя | - | - |

## Пример запроса

```shell script
 curl --request POST \
 --url 'https://<FAPI_HOST>/api/v1?name=resolveProductReviewPaymentOffers' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"productIds": [12345]}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveProductReviewPaymentOffers",
      "result": [
        12345
      ]
    }
  ],
  "collections": {
    "paymentOffer": [
      {
        "amount": 555,
        "entityId": 12345,
        "entityType": "MODEL_GRADE",
        "userId": "1122334455",
        "userType": "UID",
        "payerId": "ROV4I",
        "payerType": "VENDOR"
      }
    ]
  }
}
```


## Ссылки
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveProductReviewPaymentOffers/v1/index.js#)
- [Микроформат сущности paymentOffer](https://github.yandex-team.ru/market/microformats/blob/master/paymentOffer/paymentOffer.json)
- [Описание сущности `paymentOffer` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/paymentOffer/index.js)

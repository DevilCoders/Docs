# Резолвер resolveCpaOffers

## Описание
Возвращает cpa оффер по id модели

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `productIds`* | number[] | массив id моделей | - | - |
| `billingZone` | string | псевдоним для pp репорта. Подробнее в ссылках | default | - |

\* - обязательный параметр

## Пример запроса

```
curl --request POST \
  --url '<FAPI host>api/v1?name=resolveCpaOffers' \
  --header 'content-type: application/json' \
  --data '{
    "params": [{
        "productIds": [13584121, 1759344103]
    }]
}'
```

## Пример ответа

```
{
  "results": [
    {
      "handler": "resolveWishlistTags",
      "result": string[] // массив с id офферов
    }
  ],
  "collections": {
    "offer": type Offer[] // массив оферов
  }
}

```

## Полезные ссылки
[Доступные billingZone](https://github.yandex-team.ru/market/marketfront/blob/master/src/resources/report/params/billingZone.js#L7)
[Тип оффер](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/offer/index.js)

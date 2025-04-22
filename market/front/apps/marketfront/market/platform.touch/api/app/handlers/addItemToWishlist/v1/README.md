# Резолвер addItemToWishlist

## Описание

Резолвер, добавляющий сущность(product или offer) в Wishlist:
```
    type: 'model' | 'offer',
    itemId: string (id сущности)
    displayName: string,
    hid: number,
    modelId: number (id модели),
```

Обязательные параметры:
 - type: 'model' | 'offer',
 - itemId: string (id сущности)
 - hid: number


Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addItemToWishlist/v1/constraints.js)

Возвращает нормализованные данные
```
{
  "results": [
    {
      "handler": "addItemToWishlist",
      "result": [
        "234289042"
      ]
    }
  ],
  "collections": {
    "wishlist": [
      {
        "id": "234289042",
        "displayName": "Наушники Sony MDR-XB50AP",
        "type": "model",
        "itemId": "10818816",
        "tags": [
          "234289043"
        ],
        "createDate": 1574374974202,
        "hid": "90555"
      }
    ]
  }
}
```

# PersStatic

Пример отзыва (встречается в виде терминов `opinion` и `review`):

```json
{
  "entity": "opinion",
  "id": "59871108",
  "type": 0,
  "created": 1542273675000,
  "anonymous": 0,
  "comment": "Всё очень медленно",
  "user": {
    "entity": "user",
    "uid": 462703116
  },
  "averageGrade": 3,
  "photos": [],
  "grade": {
    "main": 0,
    "1": null,
    "2": null,
    "3": null
  },
  "pro": "Всё очень медленно",
  "contra": "Всё очень медленно",
  "recommend": false,
  "cpa": false,
  "votes": {
    "agree": 0,
    "reject": 0,
    "total": 0
  },
  "region": {
    "entity": "region",
    "id": 65
  },
  "factors": [],
  "shop": {
    "entity": "shop",
    "id": 774
  },
  "problem": "resolved",
  "resolved": 1,
  "orderId": null,
  "delivery": 0,
  "groupId": null
}
```

## getPersonalShopOpinions

### GET /api/opinion/user/<uid>/shop/<shopId>

Возвращает отзывы указанного пользователя на указанный магазин. У одного пользователя может быть несколько отзывов на один и тот же магазин.

Пример ответа

```json
{
  "data": {
    "opinions": [
      // отзывы
    ]
  }
}
```

## getShopDistribution

### GET /api/distribution/shop/<shopId>

Возвращает рейтинг указанного магазина. В процентах и количествах оценок.

Пример ответа

```json
{
    list: [{
        parts: [{
            percent: 0.07,
            number: 78,
            value: -2,
        },
        {
            percent: 0.03,
            number: 30,
            value: -1,
        },
        {
            percent: 0.05,
            number: 57,
            value: 0,
        },
        {
            percent: 0.08,
            number: 95,
            value: 1,
        },
        {
            percent: 0.76,
            number: 857,
            value: 2,
        }],
        total: 1117,
        id: 2,
    }],
}
```

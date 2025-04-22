# Резолвер resolvePublicUserReviews

Возвращает только прошедшие модерацию опубликованные отзывы пользователя на магазины/товары с пагинатором.
**Не умеет фильтровать** отзывы по типу (магазины/товары) и по конкретному идентификтору магазина/товара.
Данные в ответе резолвера нормализованы.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `uid`* | string | Паспортный идентификтора пользователя | - | - |
| `pageNum` | number |  Номер страницы пагинатора | 1 | - |
| `pageSize` | number| Количество элементов на странице пагинатора | 10 | - |
| `clid` | number|  | - | - |

\* - обязательный параметр

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "resolvePublicUserReviews",
      "result": [
        {
          "id": 1,
          "entity": "review"
        },
        {
          "id": "8ce295f237ae886e3706f27edecf710a266c02dd6854215d35f1854f9cbcda3a",
          "entity": "pager"
        }
      ]
    }
  ],
  "collections": {
    "review": "Array()",
    "shop": "Array()",
    "product": "Array()",
    "pager": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolvePublicUserReviews/v1/index.js)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/modelOpinion/modelOpinion.json) (**WARNING**: микроформат устаревший и может не соответствовать действительности.)
- [Описание сущности `отзыв` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/review/index.js)

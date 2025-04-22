# Резолвер resolveMyReviews

Возвращает все (в т.ч. не прошедшие модерацию) отзывы текущего пользователя на магазины/товары с пагинатором.
Может фильтровать отзывы пользователя по типу (отзывы на магазины/товары) и по индентификатору магазина/товара.\
Вместе с отзывами резолвер возвращает голоса пользователя.\
Данные в ответе резолвера нормализованы.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `subject` | string | Фильтр отзывов по типу отзыва (магазины/товары). Если не передан, то вернутся все отзывы. | - | [`'shop'`, `'product'`] |
| `resourceId` | string | Фильтр отзывов по идентификатору магазина/товара. Вместе с `resourceId` нужно передавать соответствующее значение `subject` | - | - |
| `pageNum` | number |  Номер страницы пагинатора | 1 | - |
| `pageSize` | number| Количество элементов на странице пагинатора | 10 | - |
| `clid` | number|  | - | - |

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
    "reviewUserVote": "Array()",
    "review": "Array()",
    "shop": "Array()",
    "product": "Array()",
    "pager": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/market/platform.touch/api/app/handlers/resolveMyReviews/v2/index.js#L26)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/modelOpinion/modelOpinion.json) (**WARNING**: микроформат устаревший и может не соответствовать действительности)
- [Описание сущности `отзыв` в проекте](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/src/entities/review/index.js)

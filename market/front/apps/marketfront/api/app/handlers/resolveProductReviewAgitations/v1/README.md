# Резолвер resolveProductReviewAgitations

Возвращает агитации текущего пользователя с пагинатором. Возвращает агитации пользователя, проверяя, что у пользователя
нет отзыва на связанный с агитацией товар. Также возвращает всю необходимую информацию о продукте, связанном с каждой из
выбранных агитаций.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `pageNum` | number |  Номер страницы пагинатора | 1 | - |
| `pageSize` | number| Количество элементов на странице пагинатора | 3 | - |

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveProductReviewAgitations' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveProductReviewAgitations",
      "result": {
        "agitationIds": [
          "0-410518"
        ],
        "pagerId": "5064ea6ae42b090ab798d36560625d43cc140ebf598309fdf911175059da0d06"
      }
    }
  ],
  "collections": {
    "agitation": "Array()",
    "pager": "Array()",
    "product": "Array()",
    "category": "Array()",
    "navnode": "Array()",
    "navnodePicture": "Array()",
    "vendor": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/resolveProductReviewAgitations/v1/index.js#)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/agitation/agitation.json)
- [Описание сущности `агитация` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/agitation/index.js)

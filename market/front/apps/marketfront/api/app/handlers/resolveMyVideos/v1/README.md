# Резолвер resolveMyVideos

Возвращает видео текущего авторизованного пользователя с пагинатором.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `pageNum` | number |  Номер страницы пагинатора | 1 | - |
| `pageSize` | number| Количество элементов на странице пагинатора | 10 | - |

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveMyVideos' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveMyVideos",
      "result": {
        "ugcvideoIds": [
          61987,
          61973,
          61922
        ],
        "pagerId": "534b7900"
      }
    }
  ],
  "collections": {
    "productShowPlace": "Array()",
    "product": "Array()",
    "pager": "Array()",
    "publicUser": "Array()",
    "ugcvideo": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveVideosByUid/v1/index.js#)
- [Описание сущности `ugcvideo` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/ugcvideo/index.js)

# Резолвер resolveLiveStreamViews

Возвращает количество зрителей эфира и общее число просмотров

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `videoContentId` | string | Идентификатор потока стрима | - | - |

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveLiveStreamViews&content-preview=production-once' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"videoContentId": "vravPsVYQVDI"}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
        "handler": "resolveLiveStreamViews",
        "result": {
            "id": "vravPsVYQVDI",
            "viewsCount": 66451
        }
    }
  ]
}
```

## Ссылки
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveLiveStreamViews/v1/index.js#L19)
- [Описание сущности `контент трансляции` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/liveStream/index.js)
- [Описание сущности `контент плеера` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/playerContent/index.js)

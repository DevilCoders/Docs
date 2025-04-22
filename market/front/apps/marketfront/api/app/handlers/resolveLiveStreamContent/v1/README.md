# Резолвер resolveLiveStreamContent

Возвращает данные live-трансляции

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `semanticId` | string | Идентификатор трансляции | - | - |
| `contentPreview`** | boolean | дебаг параметр для получения черновиков | - | false |

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveLiveStreamContent&content-preview=production-once' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"semanticId": "onair-demo-1"}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveLiveStreamContent",
      "result": "onair-demo-1"
    }
  ],
  "collections": {
    "liveStreamContent": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveLiveStreamContent/v1/index.js#L19)
- [Описание сущности `контент трансляции` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/liveStream/index.js)

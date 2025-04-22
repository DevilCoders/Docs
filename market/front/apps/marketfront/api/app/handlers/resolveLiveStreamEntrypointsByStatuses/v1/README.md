# Резолвер resolveLiveStreamEntrypointsByStatuses

Возвращает cms'ные страницы live-трансляций, содержищие информацию об энтрипоинтах типа LivePreview.
Страницы выбираются в зависимости от статуса трансляции.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `broadcastStatuses` | array | Статусы трансляций | - | `['onair', 'scheduled', 'finished']` |
| `isLive` | boolean | Флаг, который регулирует выдачу, основываясь на актуальности трансляций. |  | |
| `contentPreview`** | boolean | дебаг параметр для получения черновиков | - | false |

## Параметр `isLive`

Флаг, который регулирует выдачу, основываясь на актуальности трансляций.
Актуальная трансляция - это трансляция, имеющая статус "onair", или "scheduled" и времени до старта осталось меньше чем `actualBeforeStart`, или "finished" и времени с конца прошло меньше чем `actualAfterFinish`.
Если значение `isLive=true` и есть актуальные трансляции, то в ответе будут сначала актуальные, а потом все остальные.
Если значение `isLive=true` и нет актуальных трансляций, то ответ будет пустым.
Если значение `isLive=false` и есть актуальные трансляции, то ответ будет пустым.
Если значение `isLive=false` и нет актуальных трансляций, то ответ будет в обычном порядке.
Если значение `isLive` не задано, то придут все доступные по статусам трансляции.

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveLiveStreamEntrypointsByStatuses&content-preview=production-once' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"broadcastStatuses": ["onair"]}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveLiveStreamEntrypointsByStatuses",
      "result": [123]
    }
  ],
  "collections": {
    "cmsPage": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveLiveStreamEntrypointsByStatuses/v1/index.js#L12)
- [Описание сущности `LivePreview` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/liveStream/index.js)

# Резолвер saveDelayedAgitation

## Описание

Помечает агитацию как отложенную

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `agitationId` | string | Айди агитации | - |

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=saveDelayedAgitation' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"agitationId": "111"}]}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "saveDelayedAgitation",
      "result": []
    }
  ],
  "collections": {}
}
```

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/saveDelayedAgitation/v1/index.js)
- [Описание сущности `agitation` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/agitation/index.js)

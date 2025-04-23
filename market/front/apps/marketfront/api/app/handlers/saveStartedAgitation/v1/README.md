# Резолвер saveStartedAgitation

## Описание

Вызывается, если юзер начал взаимодействие с агитацией

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `agitationId` | string | Айдишник агитации | - |
| `agitationType` | number | Тип агитации | - |
| `entityId` | string | Айди сущности, на которую агитируем | - |

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=saveStartedAgitation' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"agitationId": "0-111", "agitationType": "0", "entityId": "111"}]}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "saveStartedAgitation",
      "result": []
    }
  ],
  "collections": {}
}
```

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/saveStartedAgitation/v1/index.js)
- [Описание сущности `agitation` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/agitation/index.js)

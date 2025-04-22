# Резолвер resolveFiltersDescription

## Описание

Получает информацию о фильтрах по массиву hid

## Параметры

Пользователь должен быть авторизован. На вход передаём массив объектов с названием и id

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `hidIds`* | array | Массив hid | - | - |

\* - обязательный параметр


## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>api/v1?name=resolveFiltersDescription' \
  --header 'content-type: application/json' \
  --header 'x-user-authorization: OAuth <User OAuth token>' \
  --data '{
    "params": [{
        "hidIds": [91491]
    }]
}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "resolveFiltersDescription",
      "result": []
    }
  ],
  "collections": {
    "filterDescription": Array()
  }
}

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveFiltersDescription/v1/index.js)
- [Описание сущности `описание фильтра` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/filterDescription/index.js)

```

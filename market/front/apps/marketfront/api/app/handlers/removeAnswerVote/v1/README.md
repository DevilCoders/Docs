# Резолвер removeAnswerVote

Резолвер, который позволяет удалить лайк/дизлайк на ответ. Необходима авторизация.

## Параметры
| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `answerId`* | number | Id ответа | - | - |

\* - обязательный параметр

## Пример запроса
```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=removeAnswerVote' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{
  "answerId": 1233150,
 }]}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "removeAnswerVote",
      "result": {}
    }
  ],
  "collections": {}
}
```

## Ссылки:
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/removeAnswerVote/v1/index.js#L21)

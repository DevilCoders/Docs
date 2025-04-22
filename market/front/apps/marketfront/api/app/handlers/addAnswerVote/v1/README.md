# Резолвер addAnswerVote
Резолвер, который позволяет оставить лайк/дизлайк на ответ. Необходима авторизация.

## Параметры
| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `answerId`* | number |  Id ответа | - | - |
| `vote`* | number | Оценка ответа (лайк или дизлайк) | - |  [`1` (Лайк), `-1` (Дизлайк)] |

\* - обязательный параметр

## Пример запроса
```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=addAnswerVote' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{
  "answerId": 100,
  "vote": 1
 }]}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "addAnswerVote",
      "result": {}
    }
  ],
  "collections": {}
}
```

## Ссылки:
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/addAnswerVote/v1/index.js#L21)

# Резолвер addQuestionVote
Резолвер, который позволяет оставить лайк/дизлайк на вопрос. Необходима авторизация.

## Параметры
| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `questionId`* | number | Id ответа | - | - |
| `vote`* | number | Оценка вопроса (лайк или дизлайк) | - |  [`1` (Лайк), `-1` (Дизлайк)] |

\* - обязательный параметр

## Пример запроса
```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=addQuestionVote' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{
  "questionId": 100,
  "vote": 1
 }]}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "addQuestionVote",
      "result": {}
    }
  ],
  "collections": {}
}
```

## Ссылки:
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/addQuestionVote/v1/index.js#L19)

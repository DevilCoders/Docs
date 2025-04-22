# Резолвер addQuestionVote
Резолвер, который позволяет удалить лайк/дизлайк вопроса. Необходима авторизация.

## Параметры
| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `questionId`* | number | Id вопроса | - | - |

\* - обязательный параметр

## Пример запроса
```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=removeQuestionVote' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{
  "questionId": 100
 }]}'
```

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "removeQuestionVote",
      "result": {}
    }
  ],
  "collections": {}
}
```

## Ссылки:
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/removeQuestionVote/v1/index.js#L19)

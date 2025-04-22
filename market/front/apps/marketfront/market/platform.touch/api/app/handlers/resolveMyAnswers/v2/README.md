# Резолвер resolveMyAnswers

Возвращает ответы текущего авторизованного пользователя с пагинатором.

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. Сущности в result также будут продублированы в старом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `pageNum` | number |  Номер страницы пагинатора | 1 | - |
| `pageSize` | number| Количество элементов на странице пагинатора | 10 | - |

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v2?name=resolveMyAnswers' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveMyAnswers",
      "result": [
        {
          "entity": "answer",
          "id": 1838223
        },
        {
          "entity": "product",
          "id": 11944165
        },
        {
          "entity": "user",
          "id": 151283244
        },
        {
          "entity": "publicUser",
          "id": 151283244
        },
        {
          "entity": "pager",
          "id": "4038bebfc738a14ed7ba4e6f7b6f193934e7a35ef1c59e3652b5090e19210e27"
        }
      ]
    }
  ],
  "collections": {
    "picture": "Array()",
    "category": "Array()",
    "product": "Array()",
    "user": "Array()",
    "publicUser": "Array()",
    "question": "Array()",
    "pager": "Array()",
    "answer": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveMyAnswers/v2/index.js#)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/questionAnswer/questionAnswer.json)
- [Описание сущности `ответ` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/answer/index.js)

# Резолвер resolveMyQuestions

Возвращает вопросы текущего авторизованного пользователя с пагинатором.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `pageNum` | number |  Номер страницы пагинатора | 1 | - |
| `pageSize` | number| Количество элементов на странице пагинатора | 10 | - |

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v2?name=resolveMyQuestions' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveMyQuestions",
      "result": {
        "product": [
          217317553
        ],
        "question": [
          1838130
        ],
        "pager": [
          "11cb802000170df70a88b4e0486b35562d4b04287115408552f894269aa23b40"
        ],
        "category": [
          15450081
        ],
        "picture": [
          "//avatars.mds.yandex.net/get-mpic/2016828/img_id4806054976190883129.jpeg/orig"
        ]
      }
    }
  ],
  "collections": {
    "question": "Array()",
    "pager": "Array()",
    "product": "Array()",
    "user": "Array()",
    "category": "Array()",
    "picture": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveMyQuestions/v2/index.js#)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/question/question.json)
- [Описание сущности `вопрос` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/question/index.js)

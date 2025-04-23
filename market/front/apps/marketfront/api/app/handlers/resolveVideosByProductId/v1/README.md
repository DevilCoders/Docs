# Резолвер resolveVideosByProductId

Возвращает UGC видео для указанного продукта.

Данные в ответе резолвера нормализованы.

## Параметры

Обязательный параметр _productId_.

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `productId` | number | ProductId | Идентификатор товара, к которому привязано видео | - | - |
| `pageNum` | number |  Номер страницы пагинатора | 1 | - |
| `pageSize` | number| Количество элементов на странице пагинатора | 6 | - |

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveVideosByProductId' \
 --header "Authorization: GUEST" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"productId": 12345}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveVideosByProductId",
      "result": ["12345", "56789"]
    }
  ],
  "collections": {
    "ugcvideo": "Array()",
    "user": "Array()"
  }
}
```


## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveVideosByProductId/v1/index.js#)
- [Микроформат сущности ugcvideo](https://github.yandex-team.ru/market/microformats/blob/master/ugcvideo/ugcvideo.json)
- [Описание сущности `UGC видео` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/ugcVideo/index.js)

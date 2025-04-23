# Резолвер resolveReviewPopupAgitation

Возвращает одну случайную агитацию пользователя для отображения на попапе агитаций. Проверяет что у пользователя
нет отзыва на связанную с агитацией сущность. Также возвращает всю необходимую информацию о сущности, связанной
с выбранной агитацией.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `types` | Array<AgitationType> |  Типы агитаций | - | - |
| `shouldFetchPaymentOffers` | boolean | Запрашивать ли информацию о платности агитации | - | - |

В настоящий момент поддерживаются только три типа агитаций:
* 0 - оценка на товар
* 1 - дополнить оценку на товар текстовым отзывом
* 3 - оценка на магазин

## Пример запроса

```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveReviewPopupAgitation' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --data '{"params": [{"types": [0]}]}'
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveReviewPopupAgitation",
      "result": "0-410518"
    }
  ],
  "collections": {
    "agitation": "Array()",
    "product": "Array()",
    "shop": "Array()",
    "category": "Array()",
    "navnode": "Array()",
    "navnodePicture": "Array()",
    "vendor": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/resolveReviewPopupAgitation/v1/index.js#)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/agitation/agitation.json)
- [Описание сущности `агитация` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/agitation/index.js)
- [AgitationType в Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/market/pers/author/client/src/main/java/ru/yandex/market/pers/author/client/api/model/AgitationType.java#L20)

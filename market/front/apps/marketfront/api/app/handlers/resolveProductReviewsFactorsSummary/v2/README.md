# Резолвер resolveProductReviewsFactorsSummaryV2

## Описание

Резолвер, возвращающий сущность productFactor:
1. факторы на продукт - оценки на разные факторы продукта (обычно 5 шт.)
2. % рекомендаций - сколько % людей рекомендуют этот продукт к покупке
   Единственный обязательный параметр - `productId`

**Отличие второй версии: в ответе можете получить факторы с factorType = 1**

## Пример запроса

```shell script
 curl --request POST \
 --url 'https://<FAPI_HOST>/api/v2?name=resolveProductReviewsFactorsSummary' \
 --header "Authorization: OAuth <Token>" \
 --header 'Content-Type: application/json' \
 --header 'api-platform: ANDROID' \
 --data '{"params": [{"productId":470903024,"performProductTypeCheck":true}]}'
```

## Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveProductReviewsFactorsSummary/v2/constraints.js)
- [Описание сущности `факторов на продукт` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/productFactor/index.js)

## FAQ:

> Я хочу получить отзывы для модели `7873846`. На маркете отзывы есть, а фапи ничего не возвращает. Что делать?

Возможно, это просто групповая модель.

Особенность в том, что можно оставить отзыв на каждую из модификаций отдельно,
но при просмотре на фронте нужно отображать вообще все отзывы.
Поэтому отзывы для одной из модификаций нужно запрашивать не по её `productId`, а с `parentId`, который есть у этой модели.

Для этого мы подложили соломку в виде параметра `performProductTypeCheck`. Его нужно включить, если клиент не знает
(и не может узнать) тип модели. Тогда резолвер сходит и получит модель самостоятельно.

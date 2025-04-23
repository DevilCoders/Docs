# SummaryPartnerQualityIndex (Индекс качества для магазина)

<img src="https://media.github.yandex-team.ru/user/6468/files/25a96980-fba4-11eb-941d-e4c58cca0345" width="500">

## Общее описание

Виджет отображает индекс качества магазина, отображает отключения и ограничения. Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))

| Права               | Поля из AppState | Модели  | Фичи кокона             |
| ------------------- | ---------------- | ------- | ----------------------- |
| Доступен всем ролям | -                | FBX/DBS | canShowRatingBlockForFF |

## Используемые бэкенды

-   Операционный рейтинг партнера. Описание [тут](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/cpa-controller/getPartnerRatingUsingGET)

-   Ограничение на количество заказов партнера. Описание [тут](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/cpa-controller/getOrderLimitUsingGET)

-   Получение возможности отправиться на модерацию для магазина по программе. Описание [тут](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/moderation-controller/getModerationShopProgramStatesUsingGET)

-   Получение текущего состояния программы. Описание [тут](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/feature-controller/getFeatureInfoUsingGET_1)

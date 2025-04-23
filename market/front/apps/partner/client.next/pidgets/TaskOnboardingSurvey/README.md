# TaskOnboardingSurvey (Опрос после прохождения подключения)

## Общее описание

Виджет, показывающий, сколько невыкупленных заказов будет выдано при высозе с СЦ. Используется в карусели активных задач на сводке

| Права               | Поля из AppState | Модели | Фичи кокона |
| ------------------- | ---------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`,    | Все    | -           |

## Используемые бэкенды

Достаем дату создания кампании

[searchFullCampaignInfosUsingGET](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/campaign-controller/searchFullCampaignInfosUsingGET)

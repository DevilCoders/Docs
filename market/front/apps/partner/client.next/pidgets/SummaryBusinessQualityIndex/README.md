# SummaryBusinessQualityIndex (Индекс качества для бизнеса)

<img src="https://media.github.yandex-team.ru/user/6468/files/f2fe7180-fba1-11eb-990f-14fcdf9f89af" width="500">

## Общее описание

Виджет отображает агрегированные индексы качества из магазинов бизнеса. Используется на сводке маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

| Права               | Поля из AppState | Модели  | Фичи кокона |
| ------------------- | ---------------- | ------- | ----------- |
| Доступен всем ролям | -                | FBX/DBS | -           |

## Используемые бэкенды

-   Агрегированная информация по рейтингу магазинов для бизнеса. Описание [тут](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/cpa-controller/getBusinessRatingUsingGET)

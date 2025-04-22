# SummaryBusinessAggregatedQualityIndex (Индекс качества для бизнеса)

<img src="https://media.github.yandex-team.ru/user/3761/files/1eca4f80-46db-11ec-9ada-d5b47071553e" width="500">

## Общее описание

Виджет отображает агрегированную информацию по рейтингу магазинов бизнеса. Используется на сводке маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

| Права               | Поля из AppState | Модели  | Фичи кокона |
| ------------------- | ---------------- | ------- | ----------- |
| Доступен всем ролям | -                | FBX/DBS | -           |

## Используемые бэкенды

- Агрегированная информация по рейтингу магазинов для бизнеса. Описание [тут](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/business-rating-api-controller/getAggregatedRatingsUsingGET)

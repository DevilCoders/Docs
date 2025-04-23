# SummaryBusinessOpportunities (Возможности для бизнеса)

<img src="https://media.github.yandex-team.ru/user/7930/files/65263100-e32c-11eb-84ad-abb62cb1c48d" width="500">

## Общее описание

Виджет отображает список карточек с возможностями для бизнеса партнера. Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)) и на сводке маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

Дока как настроить новый баннер [тут](https://wiki.yandex-team.ru/users/art00/business-opportunities-howto/)

| Права               | Поля из AppState | Модели  | Фичи кокона |
| ------------------- | ---------------- | ------- | ----------- |
| Доступен всем ролям | -                | FBX/DBS | -           |

## Используемые бэкенды

-   список карточек грузится из бункера по ключу market-partner/business-opportunities. Схему хранения можно посмотреть [тут](https://bunker.yandex-team.ru/market-partner/business-opportunities/.schema)

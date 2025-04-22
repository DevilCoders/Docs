# SummaryNews (Что нового на маркете - виджет новостей)

Если новость одна - отображаем новость и картинку.

<img src="https://jing.yandex-team.ru/files/endurance/Screen%20Shot%202022-02-10%20at%201.21.58%20PM.png" width="500">

Если новостей более двух, отображаем в виджете только две последние новости.

<img src="https://jing.yandex-team.ru/files/endurance/Screen%20Shot%202022-02-10%20at%201.22.40%20PM.png" width="500">

## Общее описание

Виджет, показывающий последние новости, помеченные тегом "сводка" и содержащий кнопку перехода на страницу новостей. Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)) и на сводке маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

Из настроек бункера получаем тег, новости с которым должны отображаться на сводке.

| Права               | Поля из AppState          | Модели | Фичи кокона |
| ------------------- | ------------------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`, `businessId`| FBX/DBS| -           |

## Используемые бэкенды

-   Для получения новостей: [posts](https://pages.github.yandex-team.ru/yablogs/yablogs-api-docs/v1/#список-постов-опубликованные-посты-get)

-   Также используются настройки из бункера market-partner - [news-page](https://bunker.yandex-team.ru/market-partner/settings/news-page)

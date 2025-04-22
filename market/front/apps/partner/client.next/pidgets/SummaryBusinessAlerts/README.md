# SummaryBusinessAlerts (Алерты на сводке маркетплейса)

<img src="https://media.github.yandex-team.ru/user/6468/files/d82efb80-fba7-11eb-94f6-b83f3265e551" width="600">

## Общее описание

Виджет, показывающий список алертов на сводке маркетплейса. Если алертов больше 2х добавляет выпадашку с остальными алертами. Используется на сводке маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx)). Алерты могут показываться при проблемах с магазинами бизнеса, а могут настраиваться редакторами(одновременно будет отображаться только один, самый приоритетный).

Дока как настроить новый редакторский баннер [тут](https://wiki.yandex-team.ru/users/art00/marketplace-banners-howto/)

| Права               | Поля из AppState | Фичи кокона |
| ------------------- | ---------------- | ----------- |
| Доступен всем ролям | `businessId`,    | -           |

## Как добавить новый статус

1. Добавить новый статус в константу

    - для DBS https://github.yandex-team.ru/market/partnernode/blob/master/shared/constants/partnerStatusDbs.ts
    - для остальных https://github.yandex-team.ru/market/partnernode/blob/master/shared/constants/partnerStatus.ts

2. Добавить правила вычисления нового статуса

    - для DBS https://github.yandex-team.ru/market/partnernode/blob/master/shared/utils/getDbsPartnerStatus.ts
    - для остальных https://github.yandex-team.ru/market/partnernode/blob/master/shared/utils/getPartnerStatus.ts

3. Добавить правила отрисовки ссылки/кнопки-ссылки, если нужно

    - MAP_STATUS_TO_LINK https://github.yandex-team.ru/market/partnernode/blob/master/client.next/utils/systemAlerts/constants/configs.ts

4. Добавить правила отрисовки кнопки-действия, если нужно

    - MAP_STATUS_TO_BUTTON https://github.yandex-team.ru/market/partnernode/blob/master/client.next/utils/systemAlerts/constants/configs.ts

5. Добавить в Танкер ключи для алерта

    - `pidgets.system-alerts:marketplace.${status}.title` - заголовок
    - `pidgets.system-alerts:marketplace.${status}.description` - описание
    - `pidgets.system-alerts:marketplace.${status}.button` - ссылка/кнопка-ссылка
    - `pidgets.system-alerts:marketplace.${status}.action.button` - кнопка-действие

6. Добавить в Танкер ключи для светофора

    - `shared.campaign.programs:marketplace.${status}.text`
    - `shared.campaign.programs:marketplace.${status}.tooltip`

7. Добавить новый статус в вики табличку, если ещё не добавлен

    - описание с таблицей https://wiki.yandex-team.ru/mbi/development/beru/projects/dropship-dashboard/#tablicastatusov
    - таблица отдельно https://wiki.yandex-team.ru/mbi/development/beru/projects/dropship-dashboard/program-grid/

## Как добавить кнопку к ограничительному алерту

1. Добавить правила отрисовки кнопки-действия

    - MAP_RESTRICTION_REASON_TO_BUTTON https://github.yandex-team.ru/market/partnernode/blob/master/client.next/utils/systemAlerts/constants/configs.ts

2. Добавить текст для кнопки

    - `restrictions.${reason}.action.button`

## Используемые бэкенды

Получение выручки по каждому партнёру бизнеса

[getRevenueSummaryUsingGET](https://mbi-partner-stat.tst.vs.market.yandex.net/swagger-ui.html#/marketplace-summary-controller/getRevenueSummaryUsingGET)

Получение статусов программ для партнёров внутри бизнеса

[getBusinessMarketplaceProgramsUsingPOST](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/business-program-controller/getBusinessMarketplaceProgramsUsingPOST)

Получение данных партнёров внутри бизнеса

[getPartnerMetaDTOUsingGET](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/partner-meta-controller/getPartnerMetaDTOUsingPOST)

Ограничение на количество заказов для партнеров бизнеса

[getBusinessOrderLimitsUsingGET](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/cpa-controller/getBusinessOrderLimitsUsingGET)

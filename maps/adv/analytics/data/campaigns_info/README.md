# Расчет справочника по кампаниям. Храним всю информацию, которую невозможно изменить либо важно только последнее состояние
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/adv/analytics/data/campaigns_info)

## Источники
[adv_store_production](https://yt.yandex-team.ru/hahn/navigation?path=//home/geodisplay/analytics/regular/snapshot/adv_store_production)

[billing_proxy](https://yt.yandex-team.ru/hahn/navigation?path=//home/geodisplay/analytics/regular/snapshot/billing_proxy)

[manual_orders - ручные заказы](https://yt.yandex-team.ru/hahn/navigation?path=//home/geodisplay/analytics/regular/snapshot/manual_orders/orders)

[logins - логины по author_id](https://yt.yandex-team.ru/hahn/navigation?path=//home/geoadv/geoprod/production/stream_snapshots/geoadv_users)


## Схема расчета
Джойним выгрузки бекенда геомедийки и получаем максимально полное описание рекламных кампаний

## Модель данных и описание полей

| Поле                      | Описание                                    |
|---------------------------|---------------------------------------------|
| campaign_id               | id кампании                                 |
| agency_id                 | id агентства                                |
| agency_name               | название агентства                          |
| author_id                 | id автора                                   |
| author_login              | логин автора                                |
| account_manager           | аккаунт менеджер                            |
| billing                   | формат кампании (cpm, cpa, fix)             |
| campaign_budget           | бюджет кампании                             |
| campaign_name             | название кампании                           |
| campaign_type             | рекламный формат (zsb, пины и т.д)          |
| client_id                 | id клиента                                  |
| client_name               | название клиента                            |
| contract_id               | id контракта                                |
| manual_orders_rate        | тип ручного контракта (платный, бесплатный) |
| dates_of_annual_contract  | даты начала и конца годового контракта      |
| cpa                       | cost per action                             |
| cpm                       | cost per mille                              |
| currency                  | валюта                                      |
| counterparty_id           | id контрагента                              |
| counterparty_name         | название контрагента                        |
| daily_budget              | дневной бюджет                              |
| end_date                  | дата окончания кампании                     |
| end_datetime              | время окончания кампании                    |
| external_id               | внешний id                                  |
| is_auto_daily_budget      | TRUE, если автоматический дневной бюджет    |
| is_manual                 | TRUE, если ручная кампания                  |
| limit_display_probability |                                             |
| oracle_id                 |                                             |
| order_id                  | id заказа                                   |
| platforms                 | платформы, где показывается кампания        |
| product_id                | id продукта                                 |
| publication_envs          | окружения (прод, тест)                      |
| rubric                    | рубрика                                     |
| macroindustry             | индустрия                                   |
| service_id                |                                             |
| start_date                | дата начала кампании                        |
| start_datetime            | время начала кампании                       |
| status                    | последний актуальный статус кампании        |
| targeting                 | таргетинги                                  |
| timezone                  | часовой пояс кампании                       |
| limit_impressions_per_day | лимит показов на пользователя               |
| limit_impressions_total   | дневной лимит показов на пользователя       |





## К кому можно обращаться с вопросами

Вопросы можно задавать aladgou@

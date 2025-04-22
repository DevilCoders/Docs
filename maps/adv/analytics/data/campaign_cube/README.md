# Расчет ежедневной статистики по кампаниям
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/adv/analytics/data/campaigns_cube)

## Источники
[adv_store_production](https://yt.yandex-team.ru/hahn/navigation?path=//home/geodisplay/analytics/regular/snapshot/adv_store_production)

[campaign_statistics_all](https://yt.yandex-team.ru/hahn/navigation?path=//home/geodisplay/analytics/regular/pin_shows/campaign_statistics/all)

[campaigns_info](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/adv/analytics/data/campaigns_info)

## Схема расчета
Джойним выгрузки бекенда геомедийки и получаем ежедневную статистику по всем кампаниям

## Модель данных и описание полей

| Поле                      | Описание                                 |
|---------------------------|------------------------------------------|
| campaign_id               | id кампании                              |
| fielddate                 | дата                                     |
| campaign_name             | название кампании                        |
| campaign_type             | рекламный формат (zsb, пины и т.д)       |
| platforms                 | платформы, где показывается кампания     |
| status                    | статус на fielddate                      |
| currency                  | валюта                                   |
| counterparty_id           | id контрагента                           |
| counterparty_name         | название контрагента                     |
| client_name               | название клиента                         |
| agency_name               | название агенства                        |
| order_id                  | id заказа                                |
| is_manual                 | TRUE, если ручная кампания               |
| manual_orders_rate        | тип ручного заказа (платный, бесплатный) |
| account_manager           | аккаунт менеджер                         |
| macroindustry             | индустрия                                |
| start_date                | дата начала кампании                     |
| end_date                  | дата окончания кампании                  |
| cpa                       | cost per action                          |
| cpm                       | cost per mille                           |
| daily_budget              | дневной бюджет                           |
| is_auto_daily_budget      | TRUE, если автоматический дневной бюджет |
| campaign_budget           | бюджет кампании                          |
| limit_impressions_per_day | лимит показов на пользователя            |
| limit_impressions_total   | дневной лимит показов на пользователя    |
| limit_display_probability |                                          |
| shows                     | количество показов                       |
| accepted_shows            | количество зачтенных показов             |
| accepted_shows_cost       | стоимость зачтенных показов              |
| taps                      | количество кликов                        |
| accepted_taps             | количество зачтенных кликов              |
| accepted_taps_cost        | стоимость зачтенных кликов               |
| calls                     | количество звонков                       |
| accepted_calls            | количество зачтенных звонков             |
| accepted_calls_cost       | стоимость зачтенных звонков              |
| opensites                 | количество открытий сайта                |
| accepted_opensites        | количество зачтенных открытий сайта      |
| accepted_opensites_cost   | стоимость зачтенных открытий сайта       |
| routes                    | количество маршрутов                     |
| accepted_routes           | количество зачтенных маршрутов           |
| accepted_routes_cost      | стоимость зачтенных маршрутов            |
| searches                  | количество переходов на сайт             |
| accepted_searches         | количество зачтенных переходов на сайт   |
| accepted_searches_cost    | стоимость зачтенных переходов на сайт    |





## К кому можно обращаться с вопросами

Вопросы можно задавать aladgou@

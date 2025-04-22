# Заказы такси из карт
Расчет готовит табличку на YT, содержащую заказы такси за карт. Одна строка - один фактический заказ (не обязательно успешно завершенный), поступивший в Такси из карт.


## Таблица на YT
| Название | Путь |
|---|---|
| orders | [maps/analytics/datasets/taxi-orders](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/taxi-orders) |

## Примеры расчетов по датасету

TODO

## Отчеты и дашборды по датасету

TODO


## Основная информация
Источником данных по заказам служит таблица на YT: [fct_order](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/taxi-dwh/cdm/marketplace/fct_order).

Источником названий и id источников из карт служит табличка-справочник на YT: [clid_report](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/taxi-dwh/raw/referral_partner/clid_report/clid_report)

## Делаем в рамках задачи
https://st.yandex-team.ru/GEOANALYTICS-1503

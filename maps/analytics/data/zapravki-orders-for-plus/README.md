# Ежедневная загрузка в месячные партиции для плюса
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi-dwh/import/zapravki/order)


## Источники
- [Датасет АЗС](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/datasets/azs/last)

- [Датасет заказов заправок](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/datasets/zapravki-orders)


## Схема расчета
Заказы заправок джойнятся с датасетом АЗС (потому что в выгрузке нужны координаты заказа, которых нет в датасете заказов).
Ежедневно переписывается месячная таблица.

## Модель данных и описание полей

**Описание полей**
Про таблицу рассказано в тикете https://st.yandex-team.ru/GEOANALYTICS-1486

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики Яндекс.Карт.

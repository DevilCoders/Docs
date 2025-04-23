# Агрегированная таблица транзакций
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/total-transactions)

[comment]: <> (- [Датасет в Datalens]&#40;https://datalens.yandex-team.ru/datasets/7cesbudl9mto0-zapravki-orders&#41;)

## Примеры расчетов по датасету

## Отчеты и дашборды по датасету

[Вкладка Transactions на GeoKPI](https://datalens.yandex-team.ru/np4axs3m5dk6j-geo-kpi?tab=mgX)


## Назначение
Датасет содержит данные обо всех транзакциях на картах

## Источники
[Заказы заправок](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/zapravki-orders)
[Бронирования](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/yandex-bookings)
[Такси](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/reports/money/taxi-maps-orders/all)
[Самокаты](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/scooters/report)
[Бургеркинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/curbside-pickup/orders/orders)
[Отели](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel-analytics/regular/hotels/bookings_and_redirects)


## Схема расчета
Успешные транзакции из каждого источника группируются по дням, потом объединяются в один датасет
## Модель данных и описание полей
Таблица ежедневно пересчитывается целиком.

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| `datefield` | Дата|
| 2| `orders` | Кол-во успешных транзакций|
| 3| `sum_paid_completed` | GMV |
| 4| `service_commission` | Комиссия|
| 5| `service` | Приложение (Яндекс.Карты (мобильные, веб, тач) или Нави)|
| 6| `transaction_type` | Тип транзакции|



## К кому можно обращаться с вопросами

Вопросы задавать в чат поддержки аналитики Яндекс.Карт и alyasevenyuk@ или ikolodkin@.

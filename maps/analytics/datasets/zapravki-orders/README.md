# Датасет заказов Яндекс.Заправок
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/zapravki-orders)

- [Датасет в Datalens](https://datalens.yandex-team.ru/datasets/7cesbudl9mto0-zapravki-orders)

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

*ранит данные о заказе на сервисе, информацию о пользователе и АЗС, на которой был сделан заказ

В таблице содержатся все заказы - и успешные, и завершенные с ошибкой

[comment]: <> (## Для каких сервисов считается)

[comment]: <> (* Навигатор)

[comment]: <> (* Заправки)

[comment]: <> (* Мобильные карты)

[comment]: <> (* Такометр)

## Источники

Реплика базы заказов Яндекс.Заправок  [tanker_orders](https://yt.yandex-team.ru/hahn/navigation?path=//home/zapravki/production/replica/transfer-manager/mongo/tanker_orders)

Данные о подписках Яндекс.Плюс  [user-profiles-cumulative](https://yt.yandex-team.ru/hahn/navigation?path=//home/msdata/user-profiles-cumulative/v1/last)

Данные траста о бинах банковских карт  [binbase](https://yt.yandex-team.ru/hahn/navigation?path=//home/zapravki/production/import/trust/binbase)

Данные про АЗС [azs](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/azs/2021-08-16)
## Схема расчета

Выгружаем все заказы из базы ЯндексЗаправок. Джойним с данными о плюсе, бинах и АЗС
## Модель данных и описание полей
Таблица обновляется ежедневно

**Описание полей**

|      | Поле                             | Физический смысл                                                                                |
| :--- | :------------------------------- | ----------------------------------------------------------------------------------------------- |
| 1    | order_id                         | Внутренний идентификатор заказа Яндекс.Заправок                                                 |
| 2    | puid                             | Паспортный идентификатор пользователя                                                           |
| 3    | user_id                          | Внутренний id пользователя Яндекс.Заправок                                                      |
| 4    | uuid                             | UUID пользователя                                                                               |
| 5    | device_id                        | DeviceID пользователя                                                                           |
| 6    | uuid                             | UUID пользоватея                                                                                |
| 7    | network_id                       | id сети АЗС Яндекс.Заправок                                                                     |
| 8    | network_name                     | Название сети АЗС                                                                               |
| 9    | permalink                        | Пермалинк АЗС из Справочника                                                                    |
| 10   | bonus_card_available             | Возможно ли применить карту лояльности на АЗС                                                   |
| 11   | post_pay                         | Постоплатная ли АЗС                                                                             |
| 12   | bonus_card_type                  | Тип карты лояльности, примененной в заказе                                                      |
| 13   | station_id                       | Внутренний id АЗС Яндекс.Заправок                                                               |
| 14   | station_name                     | Название АЗС                                                                                    |
| 15   | station_brand                    | Бренд АЗС                                                                                       |
| 16   | company_id                       | id компании                                                                                     |
| 17   | application                      | Приложение                                                                                      |
| 18   | platform                         | Операционная система                                                                            |
| 19   | algoritm                         | Алгоритм скидки                                                                                 |
| 20   | bank                             | Банк                                                                                            |
| 21   | card_id_yandex                   | id банковской карты                                                                             |
| 22   | card_level                       | Статус банковской карты                                                                         |
| 23   | card_pan                         | Маска карты                                                                                     |
| 24   | create_timestamp                 | Таймстемп заказа в UTC                                                                          |
| 25   | event_datetime                   | Дата и время создания заказа (МСК)                                                              |
| 26   | feadback                         | Отзыв                                                                                           |
| 27   | first_order_datetime             | Дата и время первого заказа пользователя (по Puid)                                              |
| 28   | last_order_datetime              | Дата и время предыдущего заказа пользователя (по Puid)                                          |
| 29   | orders_completed                 | Количество успешных заказов у данного пользователя, не включая текущий (по Puid)                |
| 30   | fuel_id                          | id типа топлива                                                                                 |
| 31   | litre_completed                  | Количество залитых литров                                                                       |
| 32   | geo_id                           | id наименьшего региона из геобазы                                                               |
| 33   | price_fuel                       | Цена топлива за 1 литр                                                                          |
| 34   | sum_paid_completed               | Сумма, списанная с карты пользователя                                                           |
| 35   | tips_sum_completed               | Сумма чаевых                                                                                    |
| 36   | status                           | Статус заказа (успешный = 'completed')                                                          |
| 37   | subscription_type                | Тип подписки Яндекс.Плюс                                                                        |
| 38   | user_subscription_active         | Факт наличия подписки Яндекс.Плюс                                                               |
| 39   | corp_id                          | id корпоративного клиента                                                                       |
| 40   | tips_refueller_id                | id заправщика                                                                                   |
| 41   | tips_refueller_sum_paid          | Размер чаевых, выплаченных заправщику                                                           |
| 41   | tips_sum_extra                   | Сумма доплаты заправщику от сервиса                                                             |
| 42   | order_type                       | Формат заказа, указанный пользователем.  1 - заказ в рублях, 2 - заказ в литрах, 3 - полный бак |
| 43   | topup_strategy                   | Тип начисления баллов плюса                                                                     |
| 44   | topup_value_total                | Сумма баллов плюса, начисленных за заказ                                                        |
| 45   | topup_settings_available_litre   | На сколько литров распространяется акция по начислению баллов                                   |
| 46   | topup_settings_value             | Сколько баллов за литр могло бы быть начислено за заказ                                         |
| 47   | topup_settings_limit_litre       | Сколько литров по акции плюса осталось до заказа                                                |
| 48   | price_fuel_total                 | Сумма заказа по стелле                                                                          |
| 49   | discount_station                 | Скидка от АЗС                                                                                   |
| 50   | price_fuel_station_with_discount | К оплате со скидкой от АЗС                                                                      |
| 51   | effective_discount_percentage    | Эффективная скидка %                                                                            |
| 52   | effective_discount_fix_sum       | Эффективная скидка ₽                                                                            |
| 53   | discount_service_commission      | Скидка от сервиса                                                                               |
| 54   | discount_total                   | Скидка всего                                                                                    |
| 55   | price_fuel_service_with_discount | Сумма к оплате для клиента                                                                      |
| 56   | service_commission               | Комиссия сервиса с НДС                                                                          |
| 57   | price_fuel_with_discount         | Выплачено в АЗС (сколько сервис платит в АЗС)                                                   |
| 58   | debt_sum_paid                    | Долг перед АЗС                                                                                  |
| 59   | bank_commission                  | Комиссия банка                                                                                  |
| 60   | margin_with_vat                  | Маржа с НДС                                                                                     |
| 61   | margin_without_vat               | Маржа без НДС                                                                                   |
| 62   | agent_commission                 | Агентская комиссия                                                                              |
| 63   | net_margin_with_vat              | Выручка с НДС                                                                                   |
| 64   | net_margin_without_vat           | Выручка без НДС                                                                                 |
| 65   | corp_commission                  | Комиссия корпоративного клиента                                                                 |
| 66   | tips_sum_completed               | Сумма чаевых                                                                                    |
| 67   | billing_pay_type                 |
| 68   | sum_refund_card                  | Сумма возврата пользователю                                                                     |
| 69   | corp_group                       | Тип корпоративного клиента                                                                      |
| 70   | corp_first_order_datetime        | Дата первого заказа для корп.клиента                                                            |
| 71   | corp_orders_completed            | Кол-во успешных заказов для корп.клиента                                                        |
| 72   | sbp_orders_completed             | Кол-во успешных платежей по системе быстрых платежей                                            |
| 73   | datefield                        | Дата заказа (YQL тип date)                                                                      |
| 74   | split_enabled                    | Включена ли в заказе рассрочка                                                                  |
| 75   | taxi_driver_id                   | UUID водителя такси                                                                             |
| 76   | last_split_payment_utc.          | Дата последнего ожидаемого платежа по рассрочке                                                 |
| 77   | discount_station_algoritm        | Идентификатор алгоритма скидки от АЗС                                                           |


## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или lincnitnastya@, alyasevenyuk@.

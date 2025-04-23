# Экспорт заказов (`orders/latest`)

Экспорт заказов доступен на YT по следующему пути:

[`//home/carsharing/production/data/orders/latest`](https://yt.yandex-team.ru/hahn/navigation?path=//home/carsharing/production/data/orders/latest)

## Описание схемы

`riding_price` &mdash; стоимость в статусе `riding` (в пути).
`parking_price` &mdash; стоимость в статусе `parking` (в ожидании).


## Работа с типами офферов

В зависимости от значения `offer_type`, значение полей может иметь некоторые особенности.

### `fix_point`

Представляет оффер типа `TFixPointOffer`.

Поле `total` содержит итоговый счет, который отображается в чеке у пользователя.

Для расчета полной стоимости в `riding`-е (для случая когда поездка завершилась в `finish_area`) можно использовать следующую формулу:

`pack_price + overrun_total + overtime_total - acceptance_total`

Данная формула не учитывает случай, когда машина была в статусе `parking` (такого быть не должно).

Для расчета полной стоимости в `riding`-е когда поездка **не завершилась в `finish_area`**, можно использовать следующую формулу:

`riding_total + overrun_total`

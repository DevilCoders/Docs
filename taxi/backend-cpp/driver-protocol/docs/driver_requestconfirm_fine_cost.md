# `POST /driver/requestconfirm/fine/cost`

Запрос стоимости отмены заказа водителем.

# Параметры

## В query string
- `db` - идентификатор парка
- `session` - идентификатор сессии водителя

## В теле запроса
- `order` - идентификатор заказа

# Пример
`curl -d 'order=8a3844dd2689471f9d0b5c4eaf781179' 'driver-protocol.taxi.dev.yandex.net/driver/requestconfirm/fine/cost?db=7ad36bc7560449998acbe2c57a75c293&session=191e48e4ecb446fda786386790cbe4c5'`

    {
        "sum": 0.0
    }

## Коды ответа

200 - ответ содержит стоимость отмены заказа (см. пример)

401 - невалидная сессия водителя

404 - заказ не найден

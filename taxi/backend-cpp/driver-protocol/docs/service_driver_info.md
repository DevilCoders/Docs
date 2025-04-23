# /service/driver/info

Ручка для получения информации о водителе. GET запрос.

# Параметры

- `db` - идентификатор парка
- `uuid` - идентификатор парка

# Ответ

400 - невалидный запрос

404 - водитель не найден / парк не найден / у парка не найден clid

200:

    {
        "karma_points": {
            "value": 95.1,
            "taxi_city": "Москва",
            "disable_threshold": 25.3,
            "warn_threshold": 50.7
        }
    }

 - `value` - карма, dp (driver points) водителя
 - `taxi_city` - город водителя
 - `disable_threshold`, `warn_threshold` - пороги отключения и предупреждения в соответствующем городе

либо пустой json, если у водителя отсутствует dp (driver points)


# Пример использования

`curl -v -k 'http://driver-protocol.taxi.dev.yandex.net/service/driver/info?db=c52e88b724674ef7917ee0f8fa4627de&uuid=d747e718d5484de1b09499e2f74a4bc0'`

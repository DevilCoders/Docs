# Притягивание к адресам еды

## 1. Когда и как?

При старте приложения, если пользователь не двигал пин руками и нажал на кнопку еды,
клиент отправляет запрос в /4.0/persuggest/v1/finalsuggest с добавлением request.type=eats.
Для других сервисов используем другой type.
Лавка: grocery
Аптеки: pharmacy
(на данный момент для всех type будут возвращаться адреса еды, далее поправим)
Необходимые параметры запроса:
action=pin_drop,
sticky=true,
type=a_eats,
position=<координаты из предыдущего запроса>,
в state.fields есть объект с типом "а", log и position из предыдущего ответа finalsuggest.


Полученный адрес из response.results используется для подставления в шторку еды/лавки.


## 2. Пример того, где лежит type в запросе

```json
{
    "action": "pin_drop",
    "position": [37.5, 55.71],
    "state": {
        "accuracy": 20,
        "bbox": [30.1, 50.1, 40.1, 60.1],
        "fields": [],
        "location": [37.51, 55.72],
        "coord_providers": [
            {"type": "gps", "position": [14.1234, 15.1234], "accuracy": 10.3},
            {
                "type": "platform_lbs",
                "position": [16.1, 17.1],
                "accuracy": 4.0,
            },
        ],
        "wifi_networks": [{"bssid": "a:b:c:d:e:f"}],
        "app_metrica": {"device_id": "DeviceId"},
    },
    "sticky": true,
    "type": "a_eats",
}
```

## 3. Под экспериментом

Для надежности делаем под экспериментом, так как растут запросы в persuggest, ML, eats
Эксперимент: stick_to_eats_address

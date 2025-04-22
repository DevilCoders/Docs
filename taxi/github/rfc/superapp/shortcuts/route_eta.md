# Отображение времени пути в шорткатах такси

## Продуктовая задача

Отображать время в пути для шорткатов такси

![ETA](https://jing.yandex-team.ru/files/privet/2020-02-10T15%3A15%3A01Z.png "ETA")

## Базовая логика

Cделать новую ручку (есть два варианта, см. ниже), в которую клиенты должны сходить после получения шорткатов из `v1/products`. В запросе должны быть данные из шорткатов с `.prefetch == route_eta`

В ответе ручки будет содержаться поле, которое необходимо положить в `subtitle` соотвтствующего шортката.

Отдельная ручка нужна из-за неопределенностей с таймингами роутера. Тайминги роутер-клиента canditates https://nda.ya.ru/t/dmkq_D6y3Vtsf2  показывают 100+ мс на 50 prc, однако для canditates преобладают короткие расстояния.

Если в результате работы ручки роутер продемонстрирует 50 мс на 95prc, можно будет подумать о выдаче ЕТА в запросе v1/products.

## Вариант 1 - generic-ручка получения route-eta [выбран]

Пилим новую ручку `/4.0/mlutp/v1/route-matrix`
Request: `POST /4.0/mlutp/v1/route-matrix`
```javascript
{
    "user_context": "shortcuts",  // alternative naming: intent=shortucts
    "routes": [ // required, but can be empty
        {
            // for shortcuts route == [pin_position, offers.type=taxi:expected-destination.action.point]
            "route": [[34.56, 78.90], [35.46, 87.90]],
            "id": "<id>",  // for example, shortcut-id
            "type": "auto"  // client should map taxi:expected-destination into "auto". also "drive" maps into auto as well
        },
    ]
}
```

Response:
```javascript
{
    "routes": [ // required, but can be empty
        {
            "id": "<id-from-request>",
            "eta": {
                "distance": 100, // meters
                "time": 3600, // seconds
                "display": "13 min", // depends on user_context, localization
            }
        },
    ]
}
```
Плюсы:
* Клиенты могут использовать функционал в новых клиентских фичах без бекенд-разработки (например: флоу новичка, ЕТА во время маршрута через платные дороги, поллинг на саммари, )

Минусы:
* Больше логики на клиенте (нужно понять как превратить данные на экране в запрос к дженерик-ручке, куда класть ответ) (частично справедливо и для не-дженерик ручки)
* Сложно определять логику для разных экранов (может помочь разветвление в зависимости от user_context через апи-прокси)

## Вариант 2 - ручка под шорткаты

### API

Request: `POST /4.0/shortcuts/v1/route-eta`
```javascript
{
    "position": [12.3, 45.6],  // required, pin position from v1/products request
    "shortcuts_destinations": [ // required, but can be empty
        {
            "shortuct_id": "A",  // shortuct_id from v1/products response
            "point": [42, 69]
            // ^ from from offers.[type=taxi:expected-destination].action.point
        },
        {
            "shortuct_id": "B",
            "point": [13.37, 69.5]
        },
        {
            "shortuct_id": "C",
            "point": [36.484, 69.2]
        },
        ...
    ]
}
```

Response:
```javascript
{
    "etas": [  // required, but can be empty
        {
            "shortuct_id": "A", // shortuct_id from v1/products response
            "route_eta": "12 мин" // локализованная отформатированная строка, которую нужно положить в subtitle
        },
        {
            "shortuct_id": "C",
            "route_eta": "34 мин"
        }
    ]
}
```

Важно: ручка не гарантирует ответ для каждого переданного shortcut_id.

Проблемы:
* Ручка решает общую проблему "ЕТА между точками" для конкретного юзкейса, и её можно генерализовать


### Ожидаемая нагрузка

Аналогично v1/products, ~1000 RPS

### Реализация

* Ручка будет распологаться в сервисе `shortcuts` и для расчета ETA использовать https://github.yandex-team.ru/taxi/uservices/tree/develop/libraries/client-routing через анонимную квоту.

* По словам aserebriyskiy@ для нагрузки до 5000RPS не нужна отдельная квота и можно пользоваться анонимной. Если функционал будет критичным, нужно будет договариваться отдельно.

* По конфигу ручка будет фоллбекаться на FallbackRouter (будет считать ЕТА через евклидово расстояние)

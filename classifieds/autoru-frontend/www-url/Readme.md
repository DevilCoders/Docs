# HTTP-Сервис преобразования параметров в ЧПУ

## как зовут
`af-url`

## где живет
`af-url-web.vrts-slb.test.vertis.yandex.net` – в тесте

`af-url-web.vrts-slb.prod.vertis.yandex.net` – в бою

## как работает
Сервис принимает на вход набор (массив) параметров и возвращает набор соответствующих им url.
Набор разбивается на кусочки и обрабатывается по частям, чтобы не тормозить входящие запросы.

Для добавления нового преобразования надо в [основном файле](./app/index.js) подключить [linkBuilderMiddleware](./app/middleware/linkBuilderMiddleware) и передать ему функцию преобразования и кодовое имя преобразователя, использующееся для сервисных нужд вроде мониторинга.
```javascript
app.post(
    '/params-to-url/parts/',
    linkBuilderMiddleware(partsLinkBuilder, 'parts'),
);
```

Преобразователь запускается для каждой ссылки отдельно.
В преобразватель передается имя роута, для которого надо построить ЧПУ, параметры и различные настройки вроде инфоормации о гео
```javascript
linkBuilder(
    routeName,
    params,
    {
        baseDomain: 'auto.ru',
        geo: {
            geoAlias,
            gids,
            geoOverride,
            geoSeoOverride,
        },
    },
    {
        noDomain: true,
    }
)
```

### Пример входящих данных
```json
{
    "data":[
        {
            "routeName": "listing",
            "params": {
                "categoryId":2,
                 "geo_id": 117920
             },
             "flags": {
                 "noDomain": true
             }
        },
        {
            "routeName": "listing",
            "params": {
                "categoryId":3,
                "geo_id":213
            }
        }
    ]
}
```

Параметр `routeName` может отсутствовать.

### Пример исходящих данных
```json
{
    "urls": [
        {
            "url": "https://auto.ru"
        }
    ]
}
```


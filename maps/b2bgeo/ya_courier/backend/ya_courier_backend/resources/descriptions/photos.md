# Photos

Зависимый тикет: https://st.yandex-team.ru/BBGEO-11564

# Cases
## Продуктовый кейс
1. Кейс Simple. У клиента существует проблема, что при доставке на определенную точку в первый раз надо найти, где находится вход в организацию. Они видят проблему, что если на заказ водитель едет в первый раз, то первое посещение занимает у него сильно больше времени, чем если он едет в знакомую точку. Предпологаемое решение -- курьер делает фото входа в организацию, после чего логист может переслать эти фото курьерам, которые поедут в ту же точку

## Использование
### Для курьера
1. Указать проблему на заказе (пример: невозможно найти проезд к точке)
   ```json
   POST /api/v1/internal/companies/6/orders/4/photos
    [
        {
            "link": "s3.yandex.ru/my_photo_link",
            "created_at": "2021-10-27T16:00:00+05:00",
            "point": {
                "lat": 58.3,
                "lon": 38.7
            },
            "courier_id": "3",
            "tags": [],
            "comment": "Don't have entry permission for this city, so I can't come in",
            "ttl_s": 41
        }
    ]
   ```
2. Подтверждение доставки заказа
   ```json
   POST /api/v1/internal/companies/6/orders/4/photos
    [
        {
            "link": "s3.yandex.ru/my_photo_link",
            "created_at": "2021-10-27T16:00:00+05:00",
            "point": {
                "lat": 58.3,
                "lon": 38.7
            },
            "courier_id": "3",
            "tags": ["delivery-proof"],
            "ttl_s": 41
        }
    ]
   ```
### Для логиста
1. Посмотреть фото для заказов/маршрутов
   ```
   GET /api/v1/companies/6/photos?order_ids=1,2
   GET /api/v1/companies/6/photos?route_ids=2
   ```
2. Посмотреть фотографии по какому-либо тегу (кейс Simple - можно указать тег "address")
   ```
   GET /api/v1/companies/6/photos?tag=address
   ```
### Для фронтенда
1. Удалить старые фотографии
   ```
   DELETE /api/v1/internal/companies/6/photos?ids=1
   ```
2. Получить загруженные фотографии с учетом того, что получены id
   ```
   GET /api/v1/companies/6/photos?ids=1,2
   ```
### Примечания
1. В тегах запрещаем использование следующих символов ```?&=,```
2. ttl_s - время гарантированного хранения информации о фотографии в секундах
3. route_id получаем непосредственно при загрузке фото, чтобы уменьшить вероятность ошибки при создании и не валидировать дополнительно совпадение с текущим маршрутом

# API
### GET /api/v1/companies/{company_id}/photos

Тип авторизации: blackbox

Примечание: при запросе из приложения необходимо указывать ```courier_id``` пользователя

### Фильтрации
Фильтрации по маршрутам и по заказам являются взаимоисключающеми -- можно задать только один из этих типов фильтрации. ```company_id``` является обязательным параметром. Других ограничений на фильтрации нет. 
1. По маршрутам ```?route_ids=1,2,3```
2. По заказам ```?order_ids=4,5,6```
3. По id ```?ids=7,8,9```
4. По тегу ```?tag=address```
5. По id курьера ```?courier_id=10``` </br>

Пагинация.
   1. ```page (min=1, default=1)```
   2. ```per_page (min=1, default=100, max=2000)```

| Response codes |  |
| --- | --- |
| 200 | Success, photos recieved |
| 401 | Authorization failed |
| 403 | Forbidden |
| 404 | Specified object not found |
| 422 | Client error |
| 500 | Internal error |

Success:
```json
[
    ...
    {
        "id": string,
        "link": string,
        "created_at": datetime with timezone,
        "point": {
            "lat": number,
            "lon": number
        },
        "company_id": string,
        "route_id": string,
        "courier_id": string,
        "order_id": string,
        "tags": array[string],
        "comment": Optional[string],
        "ttl_s": number
    }
    ...
]
```

Error:
```json
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```

### POST /api/v1/internal/companies/{company_id}/orders/{order_id}/photos

Тип авторизации: TVM <br>
Одним запросом можно загрузить не более 100 фотографий </br>

Request body: 
```json
[
    ...
    {
        "link": string,
        "created_at": datetime with timezone,
        "point": {
            "lat": number,
            "lon": number
        },
        "courier_id": string,
        "tags": array[string],
        "comment": Optional[string],
        "ttl_s": number
    }
    ...
]
```

| Response codes |  |
| --- | --- |
| 200 | Success, photos added |
| 401 | Authorization failed |
| 404 | Specified object not found |
| 422 | Client error |
| 500 | Internal error |

Success:
```json
[
    ...
    {
        "id": string
    },
    ...
]
```
Error:
```json
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```

Example: </br>

Request:
```json
POST /api/v1/internal/companies/6/orders/2/photos
[
    {
        "link": "s3.yandex.ru/my_photo_link",
        "created_at": "2021-10-27T16:00:00+05:00",
        "point": {
            "lat": 58.3,
            "lon": 38.7
        },
        "route_id": "1",
        "courier_id": "3",
        "ttl_s": 41
    },
    {
        "link": "s3.yandex.ru/my_photo_link",
        "created_at": "2021-10-27T16:00:00+05:00",
        "point": {
            "lat": 58.3,
            "lon": 38.7
        },
        "courier_id": "3",
        "tags": ["broken-car", "client-not-responding"],
        "comment": "Don't have entry permission for this city, so I can't come in",
        "ttl_s": 41
    }
]
```
Response:
```json
[
    {
        "id": "1"
    },
    {
        "id": "2"
    }
]
```


### DELETE /api/v1/internal/companies/{company_id}/photos

Тип авторизации: TVM <br>
Параметры: </br>
1. ```?ids=``` -- список id фото для удаления. Максимальное количество 100. Обязательный параметр.

| Response codes |  |
| --- | --- |
| 200 | Success, photos deleted |
| 401 | Invalid tvm-token |
| 404 | Specified object not found |
| 422 | Client error |
| 500 | Internal error |

Success:
```json
{}
```

Error:
```json
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```
Example:
```json
DELETE /api/v1/internal/companies/6/photos?ids=1,2,3
```

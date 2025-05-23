# Список районов

Запрос позволяет получить информацию обо всех доступных районах поездок клиента.

## Синтаксис запроса

```
GET https://business.taxi.yandex.ru/api/1.0/client/{идентификатор клиента}/geo_restrictions? 
limit=<количество записей>
&offset=<количество пропускаемых записей>
```

{% include [order-create-headers-p](../_includes/concepts/order-create/id-order-create/headers-p.md) %}


#### Authorization
OAuth-токен. Процесс получения токена описан в разделе [Начало работы](quickstart.md).

Запрос может содержать следующие необязательные аргументы:

- `limit` — количество выводимых записей. При отсутствии данного параметра возвращается информация о первых 100 записях.
    
- `offset` — количество пропускаемых записей. При отсутствии данного параметра возвращается информация начиная с первой записи.
    

Записи в ответе сортируются по дате и времени последнего обновления.

## Описание полей ответа

В ответе могут содержаться следующие поля:

Поле | Описание | Формат
----- | ----- | -----
`_id` | Идентификатор. | Строка
`name` | Имя. | Строка
`geo_type` | Тип гео ограничения. Сейчас поддерживается только «circle». | Строка
`geo` | Описание гео ограничения. Содержит следующие поля:<br/>- `center` — координаты центра;<br/>- `radius` — расстояние от центра (в метрах). | Объект


## Пример запроса

```
GET https://business.taxi.yandex.ru/api/1.0/client/7498c21b09a04172bd41472f6a7c0af3/geo_restrictions?limit=50
...
Authorization: <OAuth-токен>
```

## Пример ответа

Пример ответа на данный запрос выглядит следующим образом:

```no-highlight
{
    "limit": 50,
    "offset": 0,
    "items": [
      {
        "_id": "008157832119489bb7379f39fbdc6917",
        "geo": {
          "center": [
            72.368212,
            54.989342
          ],
          "radius": 500
        },
        "geo_type": "circle",
        "name": "Офис 1"
      },
      {
        "_id": "b45efcaa04014fff997c2683ef91f0de",
        "geo": {
          "center": [
            37.642639,
            55.734894
          ],
          "radius": 200
        },
        "geo_type": "circle",
        "name": "Офис 2"
      }
    ]
  }
```

## Возможные коды ответа

Ответ на данный запрос может содержать следующие стандартные HTTP-коды:

- `200` — запрос выполнен успешно.
- `400` — в запросе был передан неизвестный параметр.
- `401` — был передан неверный [OAuth-токен](quickstart.md).
- `403` — у клиента не хватает прав на выполнение данного запроса.


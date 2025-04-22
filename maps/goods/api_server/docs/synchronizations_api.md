# API синхронизаций

Информацию про авторизацию и коды ошибок см. в [основной доке по API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/api_server/docs/api.md).

Для одной организации возможна только одна *is_primary=true* синхронизация. Первые 10000 товаров для этой синхронизации будут переложены в источник TYCOON для модерации и публикации на Карты.

Для некоторых TVM сервисов существует возможность управлять *is_primary=false* синхронизациями вне зависимости от наличия прав на редактирование организации.

----
<h2>GET /goods/1.x/company/{permalink}/sync</h2>

Получить список синхронизаций компании

**Ответ**:
```json
{
    "items": [
        {
            "id": "1",
            "name": "Синхронизация 1",
            "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
            "is_enabled": true, // включена ли синхронизация
            "is_primary": true, // использовать в качестве источника в ЛК, значение true может быть только для одной синхронизации в организации
            "file_type": "Yml", // тип файла Yml
            "is_tried_to_sync": true, // производилась ли синхронизация с момента редактирования
            "status": { // статус последней синхронизации, опционально
                "sync_time": "2022-02-18T12:00:52.868836000Z",
                "sync_state": "Warning", // Success, Failed, Warning
                "message": "Warning: Слишком длинное описание товара (offer_id=12)",
                "file_url": "https://maps-geoapp-goods-synchronizations-stable.s3.yandex.net/price-list.xml", // публичная ссылка на файл
                "parse_info": {
                    "total_items_count": 10,
                    "parsed_items_count": 10,
                    "items_with_photo_count": 5
                },
                "changes_info": {
                    "added_items_count": 10,
                    "changed_items_count": 0,
                    "deleted_items_count": 0
                }
            }
        },
        ...
    ]
}
```

----
<h2>GET /goods/1.x/company/{permalink}/sync/{sync-id}</h2>

Получить синхронизацию компании с историей

**Параметры**:
| **Название** | **тип** | **описание** |
| ------------ | ------- | ------------ |
| limit | uint | ограничение на кол-во записей истории в ответе. По умолчанию: 10 (не более 10000) |

**Ответ**:
```json
{
    "id": "1",
    "name": "Синхронизация 1",
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "is_enabled": true, // включена ли синхронизация
    "is_primary": true, // использовать в качестве источника в ЛК
    "file_type": "Yml", // тип файла Yml
    "is_tried_to_sync": true, // производилась ли синхронизация с момента редактирования
    "history": {
        "items": [ // история последних 10 синхронизаций (параметр limit)
            {
                "sync_time": "2022-02-18T12:00:52.868836000Z",
                "sync_state": "Warning", // Success, Failed, Warning
                "message": "Warning: Слишком длинное описание товара (offer_id=12)",
                "file_url": "https://maps-geoapp-goods-synchronizations-stable.s3.yandex.net/price-list.xml", // публичная ссылка на файл
                "parse_info": {
                    "total_items_count": 10,
                    "parsed_items_count": 10,
                    "items_with_photo_count": 5
                },
                "changes_info": {
                    "added_items_count": 10,
                    "changed_items_count": 0,
                    "deleted_items_count": 0
                }
            },
            ...
        ]
    }
}
```

----
<h2>POST /goods/1.x/company/{permalink}/sync</h2>

Создать синхронизацию

**Запрос**:
```json
{
    "name": "Синхронизация 1",
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "is_enabled": true, // включена ли синхронизация
    "is_primary": true, // использовать в качестве источника в ЛК
    "file_type": "Yml" // тип файла Yml
}
```

**Ответ**:
```json
{
    "id": "1",
    "name": "Синхронизация 1",
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "is_enabled": true, // включена ли синхронизация
    "is_primary": true, // использовать в качестве источника в ЛК
    "file_type": "Yml", // тип файла Yml
    "is_tried_to_sync": false, // производилась ли синхронизация с момента редактирования
    "status": null
}
```

----
<h2>PUT /goods/1.x/company/{permalink}/sync/{sync-id}</h2>

Отредактировать синхронизацию

**Запрос**:
```json
{
    "name": "Синхронизация 1",
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "is_enabled": true, // включена ли синхронизация
    "is_primary": true, // использовать в качестве источника в ЛК
    "file_type": "Yml" // тип файла Yml
}
```

**Ответ**:
```json
{
    "id": "1",
    "name": "Синхронизация 1",
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "is_enabled": true, // включена ли синхронизация
    "is_primary": true, // использовать в качестве источника в ЛК
    "file_type": "Yml", // тип файла Yml
    "is_tried_to_sync": false, // производилась ли синхронизация с момента редактирования
    "status": null
}
```

----
<h2>DELETE /goods/1.x/company/{permalink}/sync/{sync-id}</h2>

Удалить синхронизацию

**Коды ответов:**
 - 200 - успешно
 - 204 - синхронизации не существует
 - 422 - невалидный формат параметров. Подробности в описании ошибки

----
<h2>POST /goods/1.x/company/{permalink}/sync/{sync-id}/force</h2>

Ускорить синхронизацию.
Следующая попытка синхронизации будет произведена независимо от того,
когда была произведена прошлая попытка синхронизации.

**Коды ответов:**
 - 200 - успешно
 - 422 - невалидный формат параметров. Подробности в описании ошибки

----
<h2>POST /goods/1.x/company/{permalink}/sync/test</h2>

Проверить синхронизацию без сохранения

**Запрос**:
```json
{
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "file_type": "Yml" // тип файла Yml
}
```
**Ответ**:
```json
{
    "id": "1", // id проверки
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "file_type": "Yml", // тип файла Yml
    "status": {
        "sync_state": "Waiting",
        "message": null,
        "parse_info": null
    }
}
```

----
<h2>GET /goods/1.x/company/{permalink}/sync/test/{sync_test_id}</h2>

Получить статус проверки синхронизации

**Ответ**:
```json
{
    "id": "1", // id проверки
    "url": "https://example.com/price-list.yml", // ссылка на файл с товарами
    "file_type": "Yml", // тип файла Yml
    "status": {
        "sync_state": "Warning", // статус проверки Success, Failed, Warning
        "message": "Warning: Слишком длинное описание товара (offer_id=12)",
        "parse_info": {
            "total_items_count": 10, // количество найденных товаров в файле
            "parsed_items_count": 10, // количество добавляемых товаров
            "items_with_photo_count": 5 // количество добавляемых товаров с фотографиями
        }
    }
}
```

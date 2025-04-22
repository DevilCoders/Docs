# Группы товаров
Ключ в стейте `vendorModelsPromotionGroups`.

**Структура стейта**
```js
    // Список групп
    [
        {
            "id": 1502,
            "groupName": "Умные часы",
            "totalModels": 3,
            "modelsId": [
                71308760,
                217316699,
                14255398
            ]
        }
    ]
```

#### GET `/vendors/<vendorId>/modelbids/promotion/groups`

Возвращает список всех групп вендора.

##### Ответ
- result `<Object>` - результат работы ручки
    - items `<Object[]>`- список групп
- errors `<Array[Object]>` - список ошибок

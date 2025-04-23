## GET `/anomalies`
Возвращает список аномалий, частично или полностью пересекающихся с интервалом  `[from_ts, to_ts]`. 
Поддерживает пагинацию с сортировкой по полю `start_ts` аномалий.

request parameters:
```python
{
    "from_ts": 1570107730,  # unix-timestamp начала интересующего интервала
    "to_ts": 1570107750,  # unix-timestamp конца интересующего интервала
    "status": "string"  # Одно из: "created", "confirmed", "rejected"

    # пагинация
    "limit": 100,  # ограничение на длину итогового списка
    "offset": 100  # смещение от начала
    
    # возможно будут добавлены разрезы по application_platform и city, tariff
}
```
response:
Список с объектами аномалий (см. ниже)
```python
{
    "anomalies": [],  # результат операции
    "pagination": {
        "total_items": 20
    }
}
```


## GET `/anomalies/<id>`
Возвращает структурку с аномалией по id
```python
{
    "_id": "string",
    "created": 1570107730,  # время создания объекта
    "updated": 1570107730,  # время последнего обновления
    "status": "string",  # Одно из: "created", "confirmed", "rejected"

    "start_ts": 1570107730,  # время начала аномалии
    "end_ts": 1570107750,  # время конца аномалии

    # Логин пользователя, который последним изменял объект.
    # При status == 'created' поле пусто (null)
    "author": "string",  
    "description": "string",  # Произвольное текстовое поле

    # TAXIADMIN-XXXX тикет с разбором инцидента
    # Обязано быть непусто при status == 'confirmed'
    "duty_task": "string",

    # Оценка потерь из-за разладки
    "losses": {
        "orders": 1000  # может быть пусто, если еще не посчитано
    }
}
```

## POST `/anomalies`
Создает новую аномалию в статусе `created`. При успехе возвращает строку с новым идентификатором
request:
```python
{
    'start_ts': 1570107730  # required
    'end_ts': 1570107750  # required

    'author': None,
    'description': None,
    'duty_task': None,
    'losses': None
}
```

## POST `/anomalies/<id>`
Обновляет поля существующей аномалии. Удаляет аномалии, которые пересекаются с обновленным объектом.

request:
```python
{
    "status": "string",  # Обязательное поле. Одно из: "confirmed", "rejected"
    "start_ts": 1570107730,  # время начала аномалии
    "end_ts": 1570107750,  # время конца аномалии
    "description": "string",  # Произвольное текстовое поле
    "duty_task": "string",  # Номер тикета с разбором аномалии в случае status == "confirmed"
}
```
response:
Возвращает список удаленных аномалий

## DELETE `/anomalies/<id>`
Безвозвратно удаляет аномалию с соответсвующим id

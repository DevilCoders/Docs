# Партнеры (employers)


Партнер определяет флоу и специальные настройки обработки заказа. Для заказов без явно заданного `employer` используется стандартный `default`

```
GET {{host_admin}}/api/admin/employer/list
```

Пример ответа

```
{
    "objects": [
        {
            "employer_id": "75dc1ec4-b0b2-4614-99e0-5f9d660b1da2",
            "employer_meta": {},
            "employer_code": "default"
        },
        {
            "employer_id": "2b73fee8-4126-4543-b39d-8280decfa803",
            "employer_meta": {},
            "employer_code": "eats"
        }
     ]
}
```

Заведение нового партнера.


```
POST {{host_admin}}/api/admin/employer/create
{
    "objects": [
        {
            "employer_meta": "",
            "employer_code": "test"
        }

    ]
}
```

Обновление данных партнера.


```
POST {{host_admin}}/api/admin/employer/update
{
    "objects": [
        {
            "employer_meta": "",
            "employer_code": "test"
        }

    ]
}
```

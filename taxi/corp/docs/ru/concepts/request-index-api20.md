# API 2.0

Для вызова методов API версии 2.0 используйте хост:

```
https://b2b-api.go.yandex.ru/integration/...
```

Ниже приведен список запросов к сервису Яндекс Такси для версии API 2.0:

Адрес запроса | Метод | Описание
----- | ----- | -----
/2.0/users | POST | [Создание нового пользователя](api20/user-create.md)
/2.0/users/{user_id} | GET | [Детальная информация о пользователе](api20/user-info.md)
/2.0/users/{user_id} | PUT | [Обновление данных пользователя](api20/user-update.md)
/2.0/users/{user_id}/archive | POST | [Архивирование пользователя](api20/user-archive.md)



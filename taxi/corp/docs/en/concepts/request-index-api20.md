# API 2.0

To call API version 2.0 methods, use the host:

```
https://b2b-api.go.yandex.ru/integration/...
```

Below is a list of requests that can be sent to Yandex Taxi for the API version 2.0:

Request URL | Method | Description
----- | ----- | -----
/2.0/users | POST | [Create a new user](api20/user-create.md)
/2.0/users/{user_id} | GET | [Detailed user information](api20/user-info.md)
/2.0/users/{user_id} | PUT | [Update user data](api20/user-update.md)
/2.0/users/{user_id}/archive | POST | [Archive a user](api20/user-archive.md)



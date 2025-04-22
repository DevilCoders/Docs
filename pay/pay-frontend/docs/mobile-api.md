# MobileAPI

Web API для нативного мобильного клиента.

Общие параметры запросов:
* `Header` - `Authorization: OAuth<token>` - Паспортный токен

#### GET /web/api/mobile/v1/user_info

Ответ:
```
{
  "status": "success",
  "code": 200,
  "data": {
    "uid": string,
    "name": string,
    "avatar": {
      "lodpiUrl": string,
      "hidpiUrl": string,
    }
  }
}
```

Если нет аватарки:
```
{
  "status": "success",
  "code": 200,
  "data": {
    "uid": string,
    "name": string,
  }
}
```

Если невалидный токен:
```
{
  "status": "fail",
  "code": 403,
  "data": {
    "message": "FORBIDDEN"
  }
}
```

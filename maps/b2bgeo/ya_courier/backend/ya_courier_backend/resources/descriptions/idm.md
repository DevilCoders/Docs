# IDM

Зависимый тикет: https://st.yandex-team.ru/BBGEO-9082

API IDMa на Wiki https://wiki.yandex-team.ru/intranet/idm/API/#add-role

<br/>

# API

 Авторизация: TVM на всех ручках

### GET /api/v1/internal/idm/info/

Возвращает JSON со списком ролей и информацией о дополнительном поле с паспортым логином.

| Response codes |  |
| --- | --- |
| 200 | Success |
| 401 | Authorization failed |
| 403 | Forbidden |
| 500 | Internal error |

Success:
```json
{
  "code": 0,
  "roles": {
    "slug": "group",
    "name": {"ru": "Группа", "en": "Group"},
    "values": {
      "superuser": {
        "name": {
          "ru": "Суперпользователь",
          "en": "Superuser"
        }
      }
    }
  },
  "fields": [
    {
      "slug": "passport_login",
      "name": {
        "ru": "Паспортный логин",
        "en": "Passport login"
      },
      "type": "charfield",
      "required": true
    }
  ]
}
```

Client error:
```json
{
  "code": number,
  "fatal": "Client error."
}
```
<br/>

### POST /api/v1/internal/idm/add-role/

Добавляет роль суперпользвателя для пользователя с логином `passport_login`, и привязывает к нему доменный логин `login`.
* Если пользователь уже имеет эту роль, возвращает 200 ОК с полем `"warning": "This user already have this role."`.
* Если пользователя с логином `passport_login` не существует, возвращает fatal.
* Если доменный логин `login` привязан к пользователю с логином отличным от `passport_login`, не вносит никаких изменений и возвращает fatal.

Запрос в формате `application/x-www-form-urlencoded`:
```json
"login": string,
"uid": string, (optional)
"role": {"group": "superuser"},
"path": "/group/superuser/",
"fields": {"passport_login": string}
```

| Response codes |  |
| --- | --- |
| 200 | Success, role added |
| 401 | Authorization failed |
| 403 | Forbidden |
| 500 | Internal error |

Success:
```json
{
  "code": 0,
  "data": 
    {"passport_login": "some-login"}
}
```

Client error/ Not found:
```json
{
  "code": number,
  "fatal": "Error message."
}
```
<br/>

### POST /api/v1/internal/idm/remove-role/

Удаляет роль суперпользователя у пользователя с логином `passport_login` и отвязывает от него доменный логин `login`.
* Если такой роли у пользователя нет, возвращает 200 ОК с полем `"warning": "This user already doesn't have this role."`.
* Если пользователя с логином `passport_login` не существует, возвращает fatal.


Запрос в формате `application/x-www-form-urlencoded`:
```json
"login": string,
"uid": string, (optional)
"role": {"group": "superuser"},
"path": "/group/superuser/",
"fields": {"passport_login": string},
"fired": 1 (optional)
```

| Response codes |  |
| --- | --- |
| 200 | Success, role removed |
| 401 | Authorization failed |
| 403 | Forbidden |
| 500 | Internal error |

Success:
```json
{
  "code": 0
}
```

Client error/ Not found:
```json
{
  "code": number,
  "fatal": "Error message."
}
```

<br/>

### GET /api/v1/internal/idm/get-all-roles/

Возвращает информацию о всех пользователях с выданными ролями.

| Response codes |  |
| --- | --- |
| 200 | Success, role added |
| 401 | Authorization failed |
| 403 | Forbidden |
| 500 | Internal error |

Success:
```json
{
  "code": 0,
  "users": [
    {
      "login": string,
      "roles": [
        [{"group": "superuser"}, {"passport_login": string}]
      ]
    },
    {
      "login": string,
      "roles": [
        [{"group": "superuser"}, {"passport_login": string}]
      ]
    },
    …
  ]
}
```

Client error:
```json
{
  "code": number,
  "fatal": "Client error."
}
```

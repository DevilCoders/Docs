## Замечания про АПИ Директории версии 10

### Создание рассылки

#### 
Пусть для домена domain в ДНС прописаны MX-записи указывающие на большую почту (например, mx.yandex.ru). Если в базе сервиса нет данных по домену domain, то пробуем создать организацию с доменом domain через ручку `organization/with-domain/`. В случае успешного запроса в коннекте будет создана организация с доменом domain, в которой пользователь maillists будет администратором. **На этом этапе домен не считается подтвержденным для организации**, например, ручка who-is вернет ошибку 404.

В случае успеха ответит 201 и сообщит идентификатор созданной организации:
```json
{
    "org_id": 3985759
}
```

Повторный вызов ручки вернет ошибку 409 Already Exists:
```json
{
    "code": "duplicate_domain",
    "message": "Domain already added into another your organization",
    "params": {
        "conflicting_org_id": 3985466
    }
}
```

Если вызвать эту ручку с одним и тем же доменом но разными X-UID, она успешно отработает при втором вызове: будет создано 2 организации с разными админами и в каждой из организаций будет добавлен неподтвержденный домен domain. Более того - с другим X-UID ручка успешно создаст организация с неподтвержденным доменом даже если у другой организации этот домен подтвержден.

В случае успешного создания организации с неподтвержденным доменом domain, через ручку `proxy/domains/` форсим домен как подтвержденный - в случае успеха домен будет закреплен за организацией и ручка who-is будет отдавать соответствующий org_id.

В один момент времени домен может быть подтвержденным только для одной организации. Если так получилось, то ручка вернет 409:
```json
{
    "code": "domain_occupied",
    "message": "Domain \"{domain}\" already occupied",
    "params": {
        "domain": "arp106.test.nonexistingdomain.ru"
    }
}
```
Аналогичный ответ будет если после успешного вызова ручки дернуть ее еще раз, т. е. ручка не идемпотентна.

### Скоупы

Формально для включения/выключения сервиса maillists:
- directory:read_services
- directory:write_services

Однако было решено не использовать ручки `POST /v10/services/{service_slug}/ready/` и `POST /v10/services/{service_slug}/{action}/` для проставления флагов `ready` и `enabled`. 

Для возможности читать данные об организации по ее идентификатору:
- directory:read_organization

Для возможности чтения и назначения депьюти
- directory:read_users
- directory:write_users

#### Создания пользователя
Забыли заголовок X-UID:
```json
{"message": "User is required for this operation", "code": "authorization-error"}
```

Указали department_id = None:
```json
{
    "code": "unhandled_exception",
    "message": "Unhandled exception: {error}",
    "params": {
        "error": "error"
    }
}
```

Создание пользователя, пример ответа:
```json
{
  "about": null, 
  "name": {
    "last": "", 
    "first": "Тестовый юзер"
  }, 
  "language": "ru", 
  "contacts": [
    {
      "synthetic": true, 
      "alias": false, 
      "main": false, 
      "type": "staff", 
      "value": "https://staff.yandex.ru/abcde?org_id=3985466&uid=1130000044720352"
    }, 
    {
      "synthetic": true, 
      "alias": false, 
      "main": true, 
      "type": "email", 
      "value": "abcde@arp106.test.nonexistingdomain.ru"
    }
  ], 
  "user_type": "user", 
  "gender": null, 
  "external_id": null, 
  "birthday": null, 
  "is_robot": false, 
  "service_slug": null, 
  "email": "abcde@arp106.test.nonexistingdomain.ru", 
  "role": "user", 
  "groups": [], 
  "timezone": "Europe/Moscow", 
  "department": {
    "members_count": 1, 
    "description": "", 
    "created": "2020-05-14T09:39:39.166024Z", 
    "aliases": [], 
    "heads_group_id": 1, 
    "org_id": 3985466, 
    "label": "all", 
    "parent_id": null, 
    "maillist_type": "inbox", 
    "uid": 1130000044715229, 
    "path": "1", 
    "removed": false, 
    "external_id": null, 
    "id": 1, 
    "name": "Все сотрудники"
  }, 
  "position": null, 
  "is_dismissed": false, 
  "nickname": "abcde", 
  "id": 1130000044720352, 
  "aliases": []
}
```

Если в организации не подтвержден ни один домен, то при попытке создать пользователя вернется ошибка 403:
```json
{
    "code": "forbidden",
    "message": "Access denied"
}
```

При попытке создания группы с алиасом, который уже занят за другой группой или пользователем вернется ошибка 409:
```json
{
    "code": "some_user_has_this_login",
    "message": "Some user already exists with login \"{login}\"",
    "params": {
        "login": "abcde"
    }
}
```

Пример ответа с информацией о группе:
```json
{
  "email": "sndr-bnc@zapravki.yandex.ru", 
  "member_of": [], 
  "id": 25, 
  "members": [
    {
      "object": {
        "about": null, 
        "name": {
          "last": "Мейлистович", 
          "first": "Мейлист"
        }, 
        "contacts": [
          {
            "synthetic": true, 
            "alias": false, 
            "main": false, 
            "type": "staff", 
            "value": "https://staff.yandex.ru/yndx-maillists?org_id=3316448&uid=327083271"
          }, 
          {
            "synthetic": true, 
            "alias": false, 
            "main": true, 
            "type": "email", 
            "value": "yndx-maillists@yandex.ru"
          }
        ], 
        "gender": null, 
        "external_id": null, 
        "user_type": "user", 
        "email": "yndx-maillists@yandex.ru", 
        "birthday": null, 
        "role": "admin", 
        "position": null, 
        "is_dismissed": false, 
        "department_id": 1, 
        "nickname": "yndx-maillists", 
        "id": 327083271, 
        "aliases": []
      }, 
      "type": "user"
    }
  ], 
  "uid": 1130000044651087
}
```

Пример выдачи ручки `/user/{uid}`. Список доступных полей: about, aliases, avatar_id, birthday, contacts, created, department, department_id, departments, email, external_id, first_name, gender, groups, id, is_admin, is_dismissed, is_enabled, is_outstaff, is_robot, karma, language, last_name, login, middle_name, name, nickname, org_id, position, position_plain, recovery_email, role, service_slug, services, timezone, updated_at, user_type.

```json
{
  "user_type": "user", 
  "timezone": "Europe/Moscow", 
  "is_dismissed": false, 
  "avatar_id": null, 
  "id": 327083271, 
  "aliases": [], 
  "contacts": [
    {
      "synthetic": true, 
      "alias": false, 
      "main": false, 
      "type": "staff", 
      "value": "https://staff.yandex.ru/yndx-maillists?org_id=3316448&uid=327083271"
    }, 
    {
      "synthetic": true, 
      "alias": false, 
      "main": true, 
      "type": "email", 
      "value": "yndx-maillists@yandex.ru"
    }
  ], 
  "service_slug": null, 
  "role": "admin", 
  "department": {
    "id": 1
  }, 
  "email": "yndx-maillists@yandex.ru", 
  "recovery_email": null, 
  "department_id": 1, 
  "is_enabled": true, 
  "is_outstaff": false, 
  "updated_at": "2020-04-29T15:24:21.816631+03:00", 
  "birthday": null, 
  "is_admin": true, 
  "groups": [
    {
      "id": 2
    }, 
    {
      "id": 25
    }, 
    {
      "id": 26
    }
  ], 
  "services": [
    {
      "name": "Yandex.Search", 
      "slug": "search"
    }, 
    {
      "name": "Яндекс.Почта", 
      "slug": "mail"
    }, 
    {
      "name": "Главная", 
      "slug": "dashboard"
    }, 
    {
      "name": "Calendar", 
      "slug": "calendar"
    }, 
    {
      "name": "{\"ru\": \"Листы рассылки\", \"en\": \"Mail Lists\"}", 
      "slug": "maillist"
    }
  ], 
  "nickname": "yndx-maillists", 
  "about": null, 
  "name": {
    "last": "Мейлистович", 
    "first": "Мейлист"
  }, 
  "language": "ru", 
  "created": "2020-04-29T12:24:15.771797Z", 
  "gender": null, 
  "org_id": 3316448, 
  "departments": [
    {
      "id": 1
    }
  ], 
  "position": null, 
  "external_id": null, 
  "is_robot": false
}
```

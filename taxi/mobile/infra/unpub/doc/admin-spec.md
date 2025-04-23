# Администрирование сервиса

### Миграция БД
`POST /system/migrate`

**Требуется роль contributor в системе.**

Выполняет все доступные миграции относительно текущей версии схемы БД. 
Все миграции прописываются в пакете migrations.

Пример курлом:

```bash
curl -X POST -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/migrate"
```

### Получение ролей юзера по токену
`GET /system/user/checkByToken`

**Query params:**

```
checkedToken=token
```
**Требуется роль reader в системе.**

Иногда для дебага нужно проверить юзера по известному токену. Ответ приходит в формате (для ролей выводится json схема):
```json
{
  "uid": "uid",
  "login": "login",
  "roles": {
    "packageRoles": [],
    "scopeRoles": [],
    "systemRoles": [],
    "otherRoles": []
  }
}
```
Пример курлом:

```bash
curl -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/user/checkByToken?checkedToken=token"
```

### Получение ролей юзера по айдишнику
`GET /system/user/checkById`

**Query params:**

```
userId=1233124124
```
**Требуется роль reader в системе.**

Иногда для дебага нужно проверить роли конкретного юзера. Ответ приходит в формате (для ролей выводится json схема):
```json
{
  "uid": "uid",
  "roles": {
    "packageRoles": [],
    "scopeRoles": [],
    "systemRoles": [],
    "otherRoles": []
  }
}
```
Пример курлом:

```bash
curl -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/user/checkById?userId=21312"
```

### Удаление роли юзера
`DELETE /system/user/remove/role`

**Query params:**

```
userId=1233124124
```
**Body:**
```json
{"role":"reader","scope":"all","unpub":"scopes"}
```
**Требуется роль contributor в системе.**

Пример курлом:

```bash
curl -X DELETE -H "Authorization: Bearer <TOKEN>" -d "{\"role\":\"reader\",\"scope\":\"all\",\"unpub\":\"scopes\"}"  "https://dart-unpub.taxi.yandex-team.ru/system/user/remove/role?userId=21312"
```

### Удаление всех ролей юзера
`DELETE /system/user/remove/allRoles`

**Query params:**

```
userId=1233124124
```
**Требуется роль contributor в системе.**

Пример курлом:

```bash
curl -X DELETE -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/user/remove/allRoles?userId=21312"
```

### Удаление всех версий пакета из Unpub-а
`DELETE /system/package/remove/<name>`

**Path params:**
```
name - имя пакета
```
**Требуется роль contributor в системе.**

Пример курлом:

```bash
curl -X DELETE -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/package/remove/<name>"
```

### Удаление одной версии пакета из Unpub-а
`DELETE /system/package/remove/<name>/version/<version>`

**Path params:**
```
name - имя пакета
version - версия пакета
```
**Требуется роль contributor в системе.**

Пример курлом:

```bash
curl -X DELETE -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/package/remove/<name>/version/<version>"
```

### Обновление одной версии пакета из внешнего Pub-а
`POST /system/package/update/<name>/version/<version>`

**Path params:**
```
name - имя пакета
version - версия пакета
```
**Требуется роль packageUpdater (обновлятель пакетов) в системе.**

Пример курлом:

```bash
curl -X POST -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/package/update/<name>/version/<version>"
```

### Изменение настройки доступности внешнего Pub-а при скачивании пакетов
`POST /system/settings/pubNet`

**Query params:**
```
available (true|false) - доступность внешнего паба
```
**Требуется роль contributor в системе.**

Пример курлом:

```bash
curl -X POST -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/settings/pubNet?available=false"
```

### Получение настройки доступности внешнего Pub-а при скачивании пакетов
`GET /system/settings/pubNet`

**Требуется роль reader в системе.**

Пример курлом:

```bash
curl -H "Authorization: Bearer <TOKEN>" "https://dart-unpub.taxi.yandex-team.ru/system/settings/pubNet"
```
Формат ответа
```json
{ "pubNetAvailability": true|false }
```

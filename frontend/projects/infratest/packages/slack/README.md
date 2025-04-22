# Обёртка для работы с Slack API

## Установка

```bash
npm install @yandex-int/si.ci.slack
```

## Пример использования

```js
const slack = require('slack');

slack.sendMessage('CHANNEL_ID', 'Сообщение');
```

## Методы

### sendMessage

Отправляет сообщение в канал или указанному пользователю.

#### Аргументы

##### channel

* Type: string

Идентификатор канала.

##### text

* Type: string

Текст сообщения.

##### thread

* Type: string

Идентификатор треда.

##### tokenKey

* Type: string

Ключ сервиса (для получения токена).

#### Пример возвращаемых данных

##### Успех 😁

```json
{
  "ok": true,
  "channel": "C1H9RESGL",
  "ts": "1503435956.000247",
  "message": {
    "text": "Here's a message for you",
    "username": "ecto1",
    "bot_id": "B19LU7CSY",
    "attachments": [
      {
        "text": "This is an attachment",
        "id": 1,
        "fallback": "This is an attachment's fallback"
      }
    ],
    "type": "message",
    "subtype": "bot_message",
    "ts": "1503435956.000247"
  }
}
```

##### Ошибка 😰

```json
{
  "ok": false,
  "error": "too_many_attachments"
}
```

### getChannel

Запрашивает данные канала.

#### Аргументы

##### channel

* Type: string

Идентификатор канала.

##### tokenKey

* Type: string

Ключ сервиса (для получения токена).

#### Пример возвращаемых данных

##### Успех 😁

```json
{
  "ok": true,
  "channel": {
    "id": "C1H9RESGL",
    "name": "busting",
    "is_channel": true,
    "created": 1466025154,
    "creator": "U0G9QF9C6",
    "is_archived": false,
    "is_general": false,
    "name_normalized": "busting",
    "is_shared": false,
    "is_org_shared": false,
    "is_member": true,
    "is_private": false,
    "is_mpim": false,
    "last_read": "1503435939.000101",
    "latest": {
      "text": "Containment unit is 98% full",
      "username": "ecto1138",
      "bot_id": "B19LU7CSY",
      "attachments": [
        {
          "text": "Don't get too attached",
          "id": 1,
          "fallback": "This is an attachment fallback"
        }
      ],
      "type": "message",
      "subtype": "bot_message",
      "ts": "1503435956.000247"
    },
    "unread_count": 1,
    "unread_count_display": 1,
    "members": [
      "U0G9QF9C6",
      "U1QNSQB9U"
    ],
    "topic": {
      "value": "Spiritual containment strategies",
      "creator": "U0G9QF9C6",
      "last_set": 1503435128
    },
    "purpose": {
      "value": "Discuss busting ghosts",
      "creator": "U0G9QF9C6",
      "last_set": 1503435128
    },
    "previous_names": [
      "dusting"
    ]
  }
}
```

##### Ошибка 😰

```json
{
  "ok": false,
  "error": "channel_not_found"
}
```

### getUser

Запрашивает нформацию о пользователе.

#### Аргументы

##### user

* Type: string

Идентификатор пользователя.

##### tokenKey

* Type: string

Ключ сервиса (для получения токена).

#### Пример возвращаемых данных

##### Успех 😁

```json
{
  "ok": true,
  "user": {
    "id": "W012A3CDE",
    "team_id": "T012AB3C4",
    "name": "spengler",
    "deleted": false,
    "color": "9f69e7",
    "real_name": "Egon Spengler",
    "tz": "America/Los_Angeles",
    "tz_label": "Pacific Daylight Time",
    "tz_offset": -25200,
    "profile": {
      "avatar_hash": "ge3b51ca72de",
      "status_text": "Print is dead",
      "status_emoji": ":books:",
      "real_name": "Egon Spengler",
      "display_name": "spengler",
      "real_name_normalized": "Egon Spengler",
      "display_name_normalized": "spengler",
      "email": "spengler@ghostbusters.example.com",
      "image_24": "https://.../avatar/e3b51ca72dee4ef87916ae2b9240df50.jpg",
      "image_32": "https://.../avatar/e3b51ca72dee4ef87916ae2b9240df50.jpg",
      "image_48": "https://.../avatar/e3b51ca72dee4ef87916ae2b9240df50.jpg",
      "image_72": "https://.../avatar/e3b51ca72dee4ef87916ae2b9240df50.jpg",
      "image_192": "https://.../avatar/e3b51ca72dee4ef87916ae2b9240df50.jpg",
      "image_512": "https://.../avatar/e3b51ca72dee4ef87916ae2b9240df50.jpg",
      "team": "T012AB3C4"
    },
    "is_admin": true,
    "is_owner": false,
    "is_primary_owner": false,
    "is_restricted": false,
    "is_ultra_restricted": false,
    "is_bot": false,
    "is_stranger": false,
    "updated": 1502138686,
    "is_app_user": false,
    "has_2fa": false,
    "locale": "en-US"
  }
}
```

##### Ошибка 😰

```json
{
  "ok": false,
  "error": "user_not_found"
}
```

### parseUsersFromChannelTopic

Запрашивает именя пользователей из топика канала.

#### Аргументы

##### channel

* Type: string

Идентификатор канала.

##### tokenKey

* Type: string

Ключ сервиса (для получения токена).

#### Пример возвращаемых данных

##### Успех 😁

```json
["Username 1", "Username 2", "Username 3"]
```

##### Ошибка 😰

```json
{
  "ok": false,
  "error": "channel_not_found"
}
```

### parseUsersFromChannelTopicCached

Обертка над методом `parseUsersFromChannelTopic`.
Распарсив топик мы получим ID пользователей, чтобы узнать логины нужны дополнительные запросы.
Запросов будет много, поэтому необходимо кэшировать.

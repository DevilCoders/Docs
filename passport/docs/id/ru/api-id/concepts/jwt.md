# JSON Web Token

JSON Web Token (JWT) — это открытый стандарт для создания токенов доступа, основанный на формате JSON.

Токены создаются сервером Яндекса, подписываются секретным ключом и передаются клиенту, который в дальнейшем использует токен для подтверждения своей личности перед своим сервером.

## Формат запроса {#inquiry}

Основной целью JSON Web Token является создание подписанного сообщения, с помощью которого пользователь обращается к сервису для доступа к ресурсам.

Запрос на получение JWT формируется следующим образом:

```
curl -H 'Authorization: OAuth AQAD-***' 'https://login.yandex.ru/info?format=jwt'
```

Описание параметров запроса можно посмотреть в разделе [Запрос информации о пользователе](../reference/request.md).

## Формат ответа {#response}

После обработки запроса пользователь получает JWT, который закодирован в base64 и подписан.

Пример подписанного сообщения:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.
eyJpYXQiOjE2MTgyMDQ1NDMsImp0aSI6ImY1YzhlMjhiLTljMzYtMTFlYi1hZDUwLTAwMjU5MDkyODk4YSIsImV0OTgzODAzNywiaXNzIjoibGueWFuZGV4LnJ1IiwidWlkIjoxMTQyMzQ1MTU4LCJsb2dpbiI6InluZHgtZWxlbmJhc2tha292YSIsInBzdWlkIjoiMS5BQWNPX2cuaDh6eFQxNGVRSFRMSURYd2s1d203dy50Uks4cIczJiVEp3IiwibmFtZSI6Ilx1MDQxNVx1MDQzYlx2MDQzNVx1MDQzZFx1MDQzMCBcdTA0MTFcdTA0MzBcdTA0NDFcdTA0M2FcdTA0MzBcdTA0M2FcdTA0M2VcdTA0MzJcdTA0MzAiLCJlbWFpbCI6InluZHgtZWxlbmJhc2tha292YUB5YW5kZXgucnUiLCJiaXJ0aGRheSI6IiIsImdlbmRlciI6bnVsbCwiZGlzcGxheV9uYW1lIjoieW5keC1lbGVuYmFza2Frb3ZhIiwiYXZhdGFyX2lkIjoiMC7wLTAifQ.
O8NEvhJ0dI0OOnZSc7Bl-TvxZ1_JDrIpb7zYRW9Nzn
```

Чтобы извлечь информацию о пользователе из base64, используйте специальную библиотеку (например, [библиотеку Python](https://pypi.org/project/PyJWT/1.4.0/)), которой в качестве параметров передается подписанное сообщение, ключ и алгоритм подписи JWT (HS256).

Пример декодированного сообщения:

```json
{ 
    u'avatar_id': u'1824/mnL6oLbL5fhaAiY42uizvUCLJI-1',
    u'birthday': u'',
    u'display_name': u'user',
    u'email': u'usere@yandex.ru',
    u'exp': 16458707859,
    u'gender': None,
    u'iat': 1618313760,
    u'iss': u'login.yandex.ru',
    u'jti': u'6ba15884-9c4c-11eb-a478-5254005dbe7b',
    u'login': u'user',
    u'name': u'<i>user</i><b> <u>\u041f\u0440\u0438\u043c\u0430\u043a\u043e</u>',
    u'psuid': u'1.AAAAfQ.Y6L7rKzy_w8aWJJu74tF9g.vAFTNxqI15bPA4A_35Dfiw',
    u'uid': 3000250009
}
```

Ниже представлено описание [стандартных полей](https://tools.ietf.org/html/rfc7519) токена.

Поле | Описание
----- | -----
iat | Unixtime выдачи JWT.
jti | Уникальный идентификатор токена.
exp | Срок действия токена.
iss | Хост, который выдал этот токен (например, login.yandex.ru).

Набор дополнительных полей зависит от прав приложения, выбранных при регистрации на [{{ service }}](https://oauth.yandex.ru/), подробнее см. раздел [Формат и состав ответа](../reference/response.md).


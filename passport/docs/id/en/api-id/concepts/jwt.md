# JSON Web Token

JSON Web Token (JWT) is an open standard for creating access tokens based on the JSON format.

Tokens are created by the Yandex server, signed with a secret key, and passed to the client, who then uses the token to verify their identity at their server.


## Request format {#inquiry}

JSON Web Token is mainly used for creating a signed message that the client can use to access service resources.

A request for JWT has the following format:

```
curl -H 'Authorization: OAuth AQAD-***' 'https://login.yandex.ru/info?format=jwt'
```

You can see the request parameters in [Requesting user information](../reference/request.md).


## Response format {#response}

After the request is processed, the user receives a JWT that is encoded in base64 and signed.

Example of a signed message:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.
eyJpYXQiOjE2MTgyMDQ1NDMsImp0aSI6ImY1YzhlMjhiLTljMzYtMTFlYi1hZDUwLTAwMjU5MDkyODk4YSIsImV0OTgzODAzNywiaXNzIjoibGueWFuZGV4LnJ1IiwidWlkIjoxMTQyMzQ1MTU4LCJsb2dpbiI6InluZHgtZWxlbmJhc2tha292YSIsInBzdWlkIjoiMS5BQWNPX2cuaDh6eFQxNGVRSFRMSURYd2s1d203dy50Uks4cIczJiVEp3IiwibmFtZSI6Ilx1MDQxNVx1MDQzYlx2MDQzNVx1MDQzZFx1MDQzMCBcdTA0MTFcdTA0MzBcdTA0NDFcdTA0M2FcdTA0MzBcdTA0M2FcdTA0M2VcdTA0MzJcdTA0MzAiLCJlbWFpbCI6InluZHgtZWxlbmJhc2tha292YUB5YW5kZXgucnUiLCJiaXJ0aGRheSI6IiIsImdlbmRlciI6bnVsbCwiZGlzcGxheV9uYW1lIjoieW5keC1lbGVuYmFza2Frb3ZhIiwiYXZhdGFyX2lkIjoiMC7wLTAifQ.
O8NEvhJ0dI0OOnZSc7Bl-TvxZ1_JDrIpb7zYRW9Nzn
```

To retrieve user information from base64, use a special library (for example, the [Python library](https://pypi.org/project/PyJWT/1.4.0/)) that receives the signed message, key, and JWT signature algorithm (HS256) as parameters.

Example of a decoded message:

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

See the description of a token's [standard fields](https://tools.ietf.org/html/rfc7519) below.

Field | Description
----- | -----
iat | Unixtime of issuing JWT.
jti | Token's unique ID.
exp | Token lifetime.
iss | The host that issued the token (for example, login.yandex.ru).


The additional fields depend on the app permissions selected when registering in [Yandex.OAuth](https://oauth.yandex.ru/). Learn more in [Response format and content](../reference/response.md).


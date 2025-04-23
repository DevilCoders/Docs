# Обновить токен

Получение токена в обмен на refresh-токен:

1. Приложение отправляет [POST-запрос с refresh-токеном](#get-token).
    
1. {{ service }} возвращает токен и новый refresh-токен в [теле ответа](#token-body).
    
{% note info %}

Основной токен может не обновиться, если оставшийся срок его жизни достаточно длительный и выдавать новый токен нет необходимости. Рекомендуем обновлять долгоживущие токены раз в три месяца.

{% endnote %}

{% include [web-client-security](../../_includes/oauth/reference/web-client/id-web-client/security.md) %}

## Обмен refresh-токена на OAuth-токен {#get-token}

Приложение отправляет refresh-токен, а также свой идентификатор и пароль в POST-запросе.

```no-highlight
POST /token HTTP/1.1
Host: oauth.yandex.ru
Content-type: application/x-www-form-urlencoded
Content-Length: <длина тела запроса>
[Authorization: Basic <закодированная строка `client_id:client_secret`>]

   grant_type=refresh_token
 & refresh_token=<refresh_token>
[& client_id=<идентификатор приложения>]
[& client_secret=<пароль приложения>]
```

#|
|| **Параметр** | **Описание** ||
|| **Обязательные параметры** ||
|| `grant_type` | Способ запроса OAuth-токена.

Если вы используете refresh-токен, укажите значение <q>refresh_token</q>. ||
|| `refresh_token` | Refresh-токен, полученный от {{ service }} вместе с OAuth-токеном. Время жизни токенов совпадает. ||
|| **Дополнительные параметры** ||
|| `client_id` | Идентификатор приложения. Доступен в [свойствах приложения]{% if lang == "ru" %}(https://oauth.yandex.ru/){% endif %}{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (нажмите название приложения, чтобы открыть его свойства).

Пароль и идентификатор приложения также можно передать в [заголовке Authorization](#auth-header). ||
|| `client_secret` | Пароль приложения. Доступен в [свойствах приложения]{% if lang == "ru" %}(https://oauth.yandex.ru/){% endif %}{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (нажмите название приложения, чтобы открыть его свойства).

Пароль и идентификатор приложения также можно передать в [заголовке Authorization](#auth-header). ||
|#

{% include [auto-code-client-auth-header](../../_includes/oauth/reference/auto-code-client/id-auto-code-client/auth-header.md) %}

## Формат ответа с токеном {#token-body}

{% include [auto-code-client-reply-desc](../../_includes/oauth/reference/auto-code-client/id-auto-code-client/reply-desc.md) %}

```javascript
200 OK
Content-type: application/json

{
  "access_token": "{{ access-token }}",
  "refresh_token": "{{ refresh-token }}",
  "token_type": "bearer",
  "expires_in": 124234123534
}
```

Ключ | Описание
----- | -----
`access_token` | OAuth-токен с запрошенными правами или с правами, указанными при регистрации приложения.
`refresh_token` | Токен, который можно использовать для [продления срока жизни](refresh-client.md) соответствующего OAuth-токена.
`token_type` | Тип выданного токена. Всегда принимает значение <q>bearer</q>.
`expires_in` | Время жизни токена в секундах. {% if audience == "internal" %}Не включается в ответ для токенов с неограниченным временем жизни.{% endif %}

Если выдать токен не удалось, то ответ содержит описание ошибки:

```javascript
{
  "error_description": "<описание ошибки>",
  "error": "<код ошибки>"
}
```

Возможные коды ошибок:

- `invalid_client` ― приложение с указанным идентификатором (параметр `client_id`) не найдено или заблокировано. Этот код также возвращается, если в параметре `client_secret` передан неверный пароль приложения.
- `invalid_grant` — неверный или просроченный refresh-токен . Этот код также возвращается, если в refresh-токен принадлежит другому приложению (не соответствует переданному client_id).
- `invalid_request` ― неверный формат запроса (один из параметров не указан, указан дважды, или передан не в теле запроса).
- `unauthorized_client` — приложение было отклонено при модерации или только ожидает ее.
- `unsupported_grant_type` ― недопустимое значение параметра `grant_type`.
- `Basic auth required` — тип авторизации, указанный в заголовке `Authorization`, отличен от `Basic`.
- `Malformed Authorization header` — заголовок `Authorization` не соответствует формату `<client_id>:<client_secret>`, или эта строка не закодирована методом base64.

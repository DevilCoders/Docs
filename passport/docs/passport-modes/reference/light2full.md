# light2full

Позволяет задать логин учетной записи и указать персональные данные, чтобы дорегистрировать [лайт-аккаунт](https://docs.yandex-team.ru/authdevguide/concepts/LiteAuth_About).


## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
https://passport.yandex.ru/passport?
mode=light2full
[& retpath=<URL>]
```
#|
|| **Параметр** | **Значение** | **Описание** ||
|| **Обязательный параметр** | | ||
|| `mode` | register | Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
|| **Дополнительный параметр** | | ||
|| `retpath` | \<URL\> | Адрес, на который пользователя следует перенаправить после завершения работы режима. Должен указываться в формате URL-encoded.

Если параметр не указан, пользователь перенаправляется на режим [passport](passport.md). ||
|#

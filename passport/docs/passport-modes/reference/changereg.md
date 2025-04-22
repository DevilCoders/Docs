# changereg

Предоставляет страницу [Редактирование персональных данных](https://passport.yandex.ru/passport?mode=changereg). На этой странице пользователь может изменить личные данные (имя, фамилию и т. д.).


## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
https://passport.yandex.ru/passport?
mode=changereg
[& retpath=<URL>]
```

#|
||**Параметр** | **Значение** | **Описание**||
||**Обязательный параметр** | |||
||`mode`|changereg|Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||**Дополнительный параметр** | |||
||`retpath`|\<URL\>|Адрес, на который пользователя следует перенаправить после завершения работы режима. Должен указываться в формате URL-encoded.

Если параметр не указан, пользователь перенаправляется на режим [passport](passport.md).||
|#
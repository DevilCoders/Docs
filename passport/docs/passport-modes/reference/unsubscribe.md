# unsubscribe

Удаляет подписку пользователя на сервис, указанный в параметрах запроса. Пользователь должен подтвердить удаление подписки, введя пароль. Если пароль для учетной записи не задан, Паспорт предлагает пользователю дорегистрироваться в режиме [postregistration](postregistration.md).

Если пользователь подписан на указанный сервис, Паспорт удаляет соответствующую запись из таблицы [subscription](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#subscription-table) базы данных системы авторизации.

{% note info %}

Подписка оформляется в режиме [subscribe](subscribe.md).

Добавлять и удалять подписки также можно с помощью запросов нового API, предназначенных для [управления подписками](https://wiki.yandex-team.ru/passport/python/api/bundle/managesids).

{% endnote %}


Подписки на некоторые сервисы (например, Яндекс.Деньги) удалять запрещено.


## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
https://passport.yandex.ru/passport/profile/unsubscribe/
[from=<короткое название сервиса>]
[& retpath=<URL>]
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Дополнительные параметры**| | ||
||`from`|<короткое название сервиса>|
Короткое название сервиса, от которого следует отписать пользователя.

{% include [request-from-sid](../_includes/reference/register/id-request/from-sid.md) %}||
||`retpath`|\<URL\>|
Адрес, на который пользователя следует перенаправить после завершения работы режима. Должен указываться в формате URL-encoded.

Если параметр не указан, пользователь перенаправляется на режим [passport](passport.md).||
|#


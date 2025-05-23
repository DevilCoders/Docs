# logout

Завершает сессию авторизованной работы пользователя, удаляя авторизационные куки из текущего браузера.

Также с помощью режима можно отозвать все куки и токены, выписанные для учетной записи. Для этого следует использовать параметр [global](#global).


## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
https://passport.yandex.ru/passport?
mode=logout
 & yu=<кука yandexuid>
[& global=<0 | 1>]
[& retpath=<URL>]
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Обязательные параметры**| | ||
||`mode`|logout|Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||`yu`|\<значение куки `yandexuid`\>|Значение куки `yandexuid`. Используется для защиты от CSRF-атак.

Если параметр не указан, пользователь будет перенаправлен на режим [passport](passport.md) и останется авторизованным.||
|| **Дополнительные параметры** | | ||
||`global`{#global}|1|Признак отзыва всех авторизационных кук, валидных для учетной записи на данный момент. Также отзываются все OAuth-токены, выданные для доступа к аккаунту.

Обрабатывается только значение «1» — отзываются все куки и токены. Остальные значения игнорируются.||
||`retpath`|\<URL\>|
Адрес, на который пользователя следует перенаправить после завершения работы режима. Должен указываться в формате URL-encoded.

Если параметр не указан, пользователь перенаправляется на режим [passport](passport.md).||
|#





# oauth

Проверяет переданный OAuth-токен и выставляет [сессионную авторизационную куку](https://docs.yandex-team.ru/authdevguide/concepts/authorization-policy-resign), если токен валидный.

Используется только ПДД и Социализацией.


## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
https://passport.yandex.ru/passport?
mode=oauth
& access_token=<OAuth-токен>
& type=<trusted-pdd-partner | trusted-social-provider>
& retpath<URL>
& error_retpath<URL>
```

#|
||**Параметр** | **Значение** | **Описание**||
||**Обязательные параметры** | |||
||`mode`|oauth|Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||`access_token`{#access-token}|\<OAuth-токен\>|Авторизующий OAuth-токен.||
||`type`{#type}|\<trusted-pdd-partner \| trusted-social-provider\>|Тип сервиса, отправляющего запрос. Поддерживаются два значения:

- «trusted-pdd-partner» — для ПДД;
- «trusted-social-provider» — для Социализации.||
||`retpath`{#retpath}|\<URL\>|Адрес, на который пользователя следует перенаправить после завершения работы режима. Должен указываться в формате URL-encoded.

Если параметр не указан, пользователь перенаправляется на режим [passport](passport.md).||
||`error_retpath`{#error-retpath}|\<URL\>|Адрес, на который необходимо перенаправить пользователя, если при работе режима возникла [ошибка](#response).

Если адрес, заданный в значении параметра, некорректен, при возникновении ошибки пользователь перенаправляется по адресу `https://passport.yandex.ru/passport?mode=auth&errnum=invalid_request`||
|#


## Формат ответа {#response}

Если авторизационная кука успешно выставлена, пользователь перенаправляется на адрес, указанный в параметре [retpath](#retpath).

Если в процессе обработки вызова возникла ошибка, Паспорт перенаправляет пользователя на адрес, указанный в параметре [error_retpath](#error-retpath). Причина ошибки описывается в значении параметра `reason`, включенного в URL.

{% include [response-error-table](../_includes/reference/changelang/id-response/error-table.md) %}

#|
|| **reason**|**Комментарий**||
||internal-exception|OAuth-сервер не отвечает, или не удается идентифицировать пользователя ПДД.||
||unknown-type|Указанное значение параметра [type](#type) не поддерживается.||
||invalid-token|
Некорректное значение параметра [access_token](#access-token) — токен не задан, невалиден или не предоставляет требуемые права.

Поддерживаются следующие права:

- `passport:auth:trusted-pdd-partner` — для ПДД;
- `passport:auth:trusted-social-provider` — для Социализации.||
|#



# admblock

Блокирует учетную запись и, при необходимости, подписку на сервис. Технически блокировка заключается в следующих действиях:

- полю базы данных `accounts.ena` присваивается значение «0»;
- полю базы данных `subscription.login_rule` для записи с указанным SID присваивается значение «0»;
- выставляется карма, обозначающая блокировку спамера (префикс 3).

{% note alert %}

Режим `admblock` устарел. Тех же результатов можно достичь, используя запросы нового API:

- [блокирование аккаунта](https://wiki.yandex-team.ru/passport/python/api/bundle/changeaccount#izmenitpriznakblokirovki);
- [изменение кармы](https://wiki.yandex-team.ru/passport/python/api/bundle/changeaccount#izmenitkarmu);
- [изменение подписки](https://wiki.yandex-team.ru/passport/python/api/bundle/managesids) (чтобы изменять поле `login_rule`, если сервис использует его).

{% endnote %}


{% include [admsubscribe-grant](../_includes/reference/admsubscribe/id-admsubscribe/grant.md) %}



## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
http://passport-internal.yandex.ru/passport?
mode=admblock
 & uid=<UID>
[& sid=<SID>
 | from=<короткое название сервиса>]
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Обязательные параметры**| | ||
||`mode`|admsubscribe|
Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||`uid`|\<UID\>|
Идентификатор пользователя в системе авторизации.||
||**Дополнительные параметры**| | ||
||`sid`{#sid}|\<SID\>|
Идентификатор сервиса, который прислал запрос на блокировку.||
||`from`{#from}|<короткое название сервиса>|
Короткое название сервиса, который прислал запрос на блокировку.

Если параметр указан одновременно с параметром `sid`, сервис будет идентифицирован по SID.||
|#

## Формат ответа {#response}
Формат XML-ответа зависит от результата обработки запроса. При отсутствии грантов режим возвращает HTML-страницу.

[Заблокирована учетная запись и подписка на сервис](#blockedsid)
[Заблокирована только учетная запись](#blocked)
[Произошла ошибка](#error)

### Заблокирована учетная запись и подписка на сервис {#blockedsid}

Даже если учетная запись будет разблокирована, пользователь не сможет авторизоваться на сервисе до изменения поля `login_rule`.

Пример ответа:

```xml
<result status="ok">
  <uid>34553433</uid>
  <ena>0</ena>
  <login_rule>0</login_rule>
  <sid>2</sid>
</result>
```

Элементы ответа:

- **uid**
  UID заблокированной учетной записи.
- **ena**
  Новое значение поля `accounts.ena`.
- **login_rule**
  Новое значение поля `subscription.login_rule` для сервиса, указанного в запросе.
- **sid**
  SID сервиса, для которого выставлено новое значение `login_rule`.

### Заблокирована только учетная запись {#blocked}

Cервис не был указан в запросе, подписки не блокируются.

Пример ответа:

```xml
<result status="ok">
  <uid>uid</uid>
  <ena>0</ena>
</result>
```

Элементы ответа:

- **uid**
  UID пользователя, подписка которого изменяется.
- **ena**
  Новое значение поля `accounts.ena`.

### Произошла ошибка {#error}

Пример ответа:

```xml
<result status="error">
  <error>unknownuid</error>
  <text>Пользователь с таким UID не найден.</text>
</result>
```

Элементы ответа:

- **error**
  Код возникшей ошибки.
- **text**
  Описание ошибки.

{% include [response-error-table](../_includes/reference/changelang/id-response/error-table.md) %}

#|
||**Код ошибки**|**Комментарий**||
||nofield|Не указано одно из обязательных полей.||
||unknownuid|Пользователь с указанным UID не найден.||
||nosubscription|Отсутствует подписка пользователя на сервис, указанный в параметрах [sid](#sid)/[from](#from).||
||interror|
{% include [response-interror](../_includes/reference/admloginrule/id-response/interror.md) %}||
|#


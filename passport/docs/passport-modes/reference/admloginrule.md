# admloginrule

Изменяет правило подписки пользователя на указанный сервис (поле базы данных [subscription.login_rule](https://docs.yandex-team.ru/authdevguide/concepts/DB_About)).

{% note alert %}

Режим `admloginrule` устарел. Команда Паспорта рекомендует использовать запрос нового API: [изменение подписки](https://wiki.yandex-team.ru/passport/python/api/bundle/managesids), в котором можно передать новое значение поля `login_rule`.

Если нужно заставить пользователя сменить пароль, отправьте запрос [изменения опций, связанных с паролем](https://wiki.yandex-team.ru/passport/python/api/bundle/changeaccount#izmenitnastrojjkiparoljaprinuditelnajasmenaotzyvavtorizaciiit.p) с параметром `is_changing_required`. Если при этом необходимо завершить все сессии пользователя и отозвать все OAuth-токены, передайте также параметр `global_logout`.

{% endnote %}


{% include [admsubscribe-grant](../_includes/reference/admsubscribe/id-admsubscribe/grant.md) %}



## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
http://passport-internal.yandex.ru/passport?
mode=admloginrule
 & uid=<UID>
 & sid=<SID>
 | from=<короткое название сервиса>
 & login_rule=<число>
[& need_change_pass=1]
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Обязательные параметры**| | ||
||`mode`|admsubscribe|
Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||`uid`|<UID пользователя>|
Идентификатор пользователя в системе авторизации.||
||`sid`|\<SID\>|
Идентификатор сервиса, для подписки на который изменяется `login.rule`.||
||`from`{#from}|<короткое название сервиса>|
Короткое название сервиса, который прислал запрос на изменение поля.

Если параметр указан одновременно с параметром `sid`, сервис будет идентифицирован по SID.||
||`login_rule`|<число>|
Число (4 байта), характеризующее доступ к сервису для учетной записи с данной подпиской.

Каждый сервис может интерпретировать значение поля по-своему. Обычно значение «0» указывает, что доступ к сервису заблокирован для данного аккаунта.||
||**Дополнительный параметр**| | ||
||`need_change_pass`|<0 \| 1 \| yes \| no \| true \| false>|
Признак необходимости сменить пароль при следующей авторизации.

Параметр обрабатывается, если одновременно выполнены следующие условия:

- значение параметра `need_change_pass` равно «1», «yes» или «true»;
- значение параметра [from](#from) равно «passport».

Если условия выполнены, режим отзывает все авторизационные куки для заданной учетной записи. При следующей авторизации пользователя Паспорт потребует сменить пароль.||
|#

## Формат ответа {#response}
Формат XML-ответа зависит от результата обработки запроса. При отсутствии грантов режим возвращает HTML-страницу.

[Поле изменено](#success)
[Произошла ошибка](#error)


### Поле изменено {#success}

Корневой элемент `<result>` содержит атрибут `status` со значением «ok».

Пример ответа:

```xml
<result status="ok">
  <uid>34553433</uid>
  <login_rule>1</login_rule>
  <sid>2</sid>
</result>
```

Элементы ответа:

- **uid**
  UID учетной записи.
- **login_rule**
  Новое значение поля `subscription.login_rule`.
- **sid**
  SID сервиса, для подписки на который выставлено новое значение `login_rule`.

### Произошла ошибка {#error}

Корневой элемент `<result>` содержит атрибут `status` со значением «error».

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
||**Номер ошибки**|**Комментарий**||
||nofield|Не указано одно из обязательных полей.||
||unknownuid|Пользователь с таким UID не найден.||
||nosubscription|У пользователя нет подписки на указанный сервис.||
||interror|
Неопределенная внутренняя ошибка Паспорта. Запрос следует повторить.||
|#


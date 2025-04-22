# admkarma

Изменяет [карму](https://docs.yandex-team.ru/authdevguide/concepts/accounts-attributes#karma) указанного пользователя.

{% note alert %}

Режим `admkarma` устарел. Команда Паспорта рекомендует использовать запрос нового API, предназначенный для [изменения кармы](https://wiki.yandex-team.ru/passport/python/api/bundle/changeaccount#izmenitkarmu).

{% endnote %}


{% include [admreg-grant](../_includes/reference/admreg/id-admreg/grant.md) %}



## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
http://passport-internal.yandex.ru/passport?
mode=admkarma
& uid=<UID>
& karma=<карма>
& prefix=<префикс кармы>
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Обязательные параметры**| | ||
||`mode`|admkarma|
Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||`uid`|\<UID\>|
Идентификатор пользователя в системе авторизации.||
||`karma`|<карма>|
Новое значение кармы.

Допустимые значения:

- 0 — пользователь не является спамером.
- 80 — пользователь считался спамером по устаревшей оценке Фродобороны. В настоящее время значение «80» пользователям не назначается.
- 85 — пользователь с высокой вероятностью является спамером.
- 100 — пользователь является спамером.

Параметр обязателен, если в запросе не указан параметр `prefix`.||
||`prefix`|<префикс кармы>|
Используемые префиксы кармы перечислены в Вики: [http://wiki.yandex-team.ru/passport/karma](http://wiki.yandex-team.ru/passport/karma).

Параметр обязателен, если в запросе не указан параметр `karma`.||
|#


## Формат ответа {#response}

Формат XML-ответа зависит от результата обработки запроса. При отсутствии грантов режим возвращает HTML-страницу.

[Карма успешно изменена](#success)
[Произошла ошибка](#error)


### Карма успешно изменена {#success}

Корневой элемент `<result>` содержит атрибут `status` со значением «ok».

Пример ответа:

```xml
<result status="ok">
  <uid>12312202001</uid>
  <karma>85</karma>
</result>
```

Элементы ответа:

- **uid**
  UID учетной записи.
- **karma**
  Новое значение кармы.

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
||**Код ошибки**|**Комментарий**||
||nofield|Не указан один из обязательных параметров.||
||unknownuid|Пользователь с указанным UID не найден.||
||interror|

{% include [response-interror](../_includes/reference/admloginrule/id-response/interror.md) %}||
|#


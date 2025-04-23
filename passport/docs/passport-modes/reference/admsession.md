# admsession

Генерирует мобильную куку по переданному OAuth-токену.

{% include [admreg-grant](../_includes/reference/admreg/id-admreg/grant.md) %}


Режим используется Jabber-сервером для авторизации пользователя в Почте. Токен, который необходимо обменять на мобильную куку, должен быть выписан для набора прав `passport:session:get_mobile`.


## Формат запроса {#request}

OAuth-токен следует передавать в HTTP-заголовке `Authorization`.

```httpget
GET /passport? mode=admsession
Host: passport-internal.yandex.ru
Authorization: OAuth vF9dft4qmT
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Обязательный параметр**| | ||
||`mode`|admsession|
Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
|#

## Формат ответа {#response}

Формат XML-ответа зависит от результата обработки запроса. При отсутствии грантов режим возвращает HTML-страницу.

[Мобильная кука сгенерирована](#success)
[Произошла ошибка](#error)

### Мобильная кука сгенерирована {#success}

Пример ответа:

```xml
<result status="ok">
    <uid>123901239</uid>
    <session>214h614H9O8h91c4XsFJg3IJ5jM84Q3uKKcY30McvXyU1ng30j1OFv2BkUHvho.nvVH5</session>
</result>
```

Элементы ответа:

#### result
Корневой элемент ответа. Атрибут `status` со значением «ok» указывает на успешную обработку запроса.
- **uid**
  UID пользователя, для которого генерируется мобильная кука.
- **session**
  Значение сгенерированной мобильной куки со сроком жизни 2 недели.

### Произошла ошибка {#error}

Пример ответа:

```xml
<result status="error">
  <error>internal-exception</error>
  <text>Internal Error</text>
</result>
```

Элементы ответа:

#### result
Корневой элемент ответа. Атрибут `status` со значением «error» указывает на ошибку.
- **error**
  Код ошибки.

- **text**
  Описание возникшей ошибки.

  {% include [response-error-table](../_includes/reference/changelang/id-response/error-table.md) %}

  #|
  ||**Код ошибки**|**Комментарий**||
  ||internal-exception| 

  {% include [response-interror](../_includes/reference/admloginrule/id-response/interror.md) %}||
  ||token-empty|В запросе отсутствует заголовок `Authorization`.||
  ||oauth-error: <HTTP-код ответа OAuth-сервера>|При попытке проверить токен OAuth-сервер вернул указанный ошибочный код HTTP-ответа.||
  ||uid-empty|OAuth-сервер не нашел соответствующий токену UID.||
  ||no-scope|Токен валидный, но не содержит набора прав `passport:session:get_mobile`.||
  |#


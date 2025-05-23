# Метод getObjectMeta

Возвращает метаданные объекта.

Метод эквивалентен методу [get](get.md), но в ответе отсутствует сам объект.

## Запрос {#request}

```
HEAD /{bucket}/{key} HTTP/2
```

### Path параметры {#path-parameters}

Параметр | Описание
----- | -----
`bucket` | Имя бакета.
`key` | Ключ объекта.


### Заголовки {#request-headers}

Используйте в запросе необходимые [общие заголовки](../common-request-headers.md).

Также в запросе можно использовать следующие заголовки:

Заголовок | Описание
----- | -----
`Range` | Определяет диапазон байт для загрузки из объекта.<br/><br/>Подробнее про заголовок Range читайте в спецификации HTTP [http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.35](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.35).
`If-Modified-Since` | Если указан, то {{ objstorage-name }} возвращает:<br/>- Объект. Если он изменялся после указанного времени.<br/>- Код 304. Если объект не изменялся после указанного времени.<br/><br/>Если в запросе одновременно присутствуют заголовки `If-Modified-Since` и `If-None-Match` и проверки по ним разрешаются как `If-Modified-Since -> true` и `If-None-Match -> false`, то {{ objstorage-name }} возвращает код 304. Подробности смотрите в [RFC 7232](https://tools.ietf.org/html/rfc7232).
`If-Unmodified-Since` | Если указан, то {{ objstorage-name }} возвращает:<br/>- Объект. Если он не изменялся с указанного времени.<br/>- Код 412. Если объект не изменялся с указанного времени.<br/><br/>Если в запросе одновременно присутствуют заголовки `If-Unmodified-Since` и `If-Match` и проверки по ним разрешаются как `If-Unmodified-Since -> false` и `If-Match -> true`, то {{ objstorage-name }} возвращает код 200 и запрошенные данные. Подробности смотрите в [RFC 7232](https://tools.ietf.org/html/rfc7232).
`If-Match` | Если указан, то {{ objstorage-name }} возвращает:<br/><br/>- Объект. Если его `ETag` совпадает с переданным.<br/>- Код 412. Если его `ETag` не совпадает с переданным.<br/><br/><br/>Если в запросе одновременно присутствуют заголовки `If-Unmodified-Since` и `If-Match` и проверки по ним разрешаются как `If-Unmodified-Since -> false` и `If-Match -> true`, то {{ objstorage-name }} возвращает код 200 и запрошенные данные. Подробности смотрите в [RFC 7232](https://tools.ietf.org/html/rfc7232).
`If-None-Match` | Если указан, то {{ objstorage-name }} возвращает:<br/><br/>- Объект. Если его `ETag` не совпадает с переданным.<br/>- Код 304. Если его `ETag` совпадает с переданным.<br/><br/><br/>Если в запросе одновременно присутствуют заголовки `If-Modified-Since` и `If-None-Match` и проверки по ним разрешаются как `If-Modified-Since -> true` и `If-None-Match -> false`, то {{ objstorage-name }} возвращает код 304. Подробности смотрите в [RFC 7232](https://tools.ietf.org/html/rfc7232).

## Ответ {#response}

### Заголовки {#response-headers}

Помимо [общих заголовков](../common-response-headers.md) вы можете увидеть в ответе заголовки, перечисленные в таблице ниже.

Заголовок | Описание
----- | -----
`x-amz-meta-*` | Пользовательские метаданные объекта, сохраненные вместе объектом.
`x-amz-storage-class` | Класс хранения объекта.<br/>Имеет значение `COLD`, если объект находится в Холодном хранилище.<br/><br/>Если объект сохранен в Стандартном хранилище, то заголовка не будет.
`x-amz-server-side-encryption` | Алгоритм шифрования, которым был зашифрован объект. Возвращается, если объект был загружен с включенным [шифрованием](../../../operations/buckets/encrypt.md).
`x-amz-server-side-encryption-aws-kms-key-id` | Идентификатор {% if audience != "internal" %}[ключа {{ kms-short-name }}](../../../../kms/concepts/key.md){% else %}ключа {{ kms-short-name }}{% endif %}. Возвращается, если объект был загружен с включенным [шифрованием](../../../operations/buckets/encrypt.md).

### Коды ответов {#response-codes}

Перечень возможных ответов смотрите в разделе [{#T}](../response-codes.md).


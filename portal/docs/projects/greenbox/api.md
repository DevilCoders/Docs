# Greenbox API

## Сервис и сеть
{% note info %}

На данный момент есть только один сервис greenbox (*возможно*, в будущем будет несколько)

{% endnote %}
-- | production | testing
:--- | :--- | :---
Сервис nanny | [portal-greenbox](https://nanny.yandex-team.ru/ui/#/services/catalog/portal-greenbox/) | [portal-greenbox-testing](https://nanny.yandex-team.ru/ui/#/services/catalog/portal-greenbox-testing/)
HTTP балансер awacs | [greenbox.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/greenbox.yandex.net/show/) | [greenbox-testing.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/greenbox-testing.yandex.net/show/)
Аппхостовый YP endpoint set | greenbox | greenbox-testing
HTTP YP endpoint set | greenbox-http | greenbox-testing-http
Сетевой макрос | \_PORTAL\_GREENBOX\_PROD\_NETS\_ | \_PORTAL\_GREENBOX\_TEST\_NETS\_
Аппхостовый бэкенд | MORDA__GREENBOX_SERVICE | MORDA__GREENBOX_SERVICE

{% note info %}

*Именем блока* является название файла экспорта **без расширения** (файлу `topnews.json` соответствует блок `topnews`)

{% endnote %}

{% note warning %}

На данный момент поддерживаются только экспорты в формате json в виде одного объекта (ключом является имя поля, значением - его значение)

{% endnote %}

## HTTP API

{% note info %}

Взаимодействие с гринбоксом через HTTP предполагается через балансер, однако для отладки может быть удобно обращаться напрямую (т.к. балансер не выдает ошибки наружу).

{% endnote %}

### Функциональные ручки

#### `POST /set`
Ручка для загрузки данных в хранилище. Загрузка предполагается в два запроса, первый - только с метаданными, чтобы проверить, нужно ли слать данные, второй - вместе с данными. Такая схема реализована для снижения нагрузки на сеть.
Входные данные:

Метаданные, передаются в параметрах url (cgi параметры):
* `filename` - имя файла экспорта
* `md5` - md5 хэш содержимого файла
* `mtime` - таймстамп времени изменения файла
* `mode` - режим подгрузки экспорта:
  * `overwrite` - перезапись, все старые данные будут удалены перед записью новых
  * `append` - дозапись, новые данные будут записаны поверх старых без их удаления

Содержимое файла экспорта, передается в теле запроса.

{% note info %}

Тело может быть пустым, тогда ручка ответит, нужен ли такой экспорт (с такими метаданными) гринбоксу, или его можно даже не слать.

{% endnote %}

Если гринбокс запущен с специальным флагом `-enable_compression`, то тело запроса можно сжимать, при этом нужно передать заголовок `Content-Encoding` с перечислением через запятую кодеров в порядке, в котором их нужно применять для расжатия. На момент написания поддерживаются два кодера, `brotli` и `gzip`.
Пример: если передан заголовок `Content-Encoding: gzip,brotli`, гринбокс перед использованием тела запроса разожмет его сначала `gzip`, потом `brotli`.

Возможные ответы ручки:
* `REJECTED: [причина]` - метаданные успешно распознаны, но признаны не актуальными. При этом сообщается причина, почему. Обычно это из-за того, что совпадает хэш либо данные старее тех, что уже есть в хранилище. Слать данные после такого ответа не имеет смысла.
* `ACCEPTED` - метаданные успешно распознаны и признаны актуальными, но тело запроса было пустым. При получении такого ответа нужно послать запрос с теми же метаданными, передав данные экспорта в теле запроса.
* `SET` - метаданные успешно распознаны и признаны актуальными, тело запроса было не пустым, было успешно расжато и передано дальше для загрузки в хранилище. Слать данные после такого ответа не имеет смысла.
* некое сообщение об ошибке, код 500

Пример: `/set?filename=example.json&md5=123123123&mtime=123123123&mode=1` с телом `{"key": "value"}`

### Служебные ручки

#### `GET /check`
Всегда отвечает `OK`

#### `GET /clear_metadata`
Трет метаданные блока в локальном кэшэ и в хранилище, тем самым инвалидирует их и позволяет записать любые поверх них. Сами данные из кэша и хранилища не удаляются.
Параметры:
* `block` - имя блока

Пример: `/clear_metadata?block=topnews`

#### `GET /get`
Возвращает значение по ключу и блоку.
Параметры:
* `block` - имя блока
* `key` - ключ

Пример: `/get?block=topnews&key=geotop_225_ru_ru`

#### `GET /get_block_age`
Возвращает "возраст" блока (время с момента его загрузки в хранилище)
Параметры:
* `block` - имя блока

Пример: `/get_block_age?block=topnews`

#### `GET /unistat`
[Юнистат ручка голована](https://wiki.yandex-team.ru/golovan/userdocs/stat-handle/)

## GRPC (Apphost) API

{% note warning %}

Все общение происходит через протобафы.

{% endnote %}

### Типы данных
[Определение типов в файле в аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/portal/morda-go/proto/morda_greenbox/morda_greenbox.proto)

#### `TMordaGreenboxGetRequest` {#TMordaGreenboxGetRequest}
```proto
message TMordaGreenboxGetRequest {
    string blockName = 1;
    string key = 2;
}
```
Сообщение для запроса одного значения по ключу и блоку.

#### `TMordaGreenboxGetResponse` {#TMordaGreenboxGetResponse}
```proto
message TMordaGreenboxGetResponse {
    string result = 1;
}
```
Ответное сообщение, содержит запрошенное значение (пустая строка, если значения в хранилище не оказалось).

#### `TMordaGreenboxGetBulkRequest` {#TMordaGreenboxGetBulkRequest}
```proto
message TMordaGreenboxGetBulkRequest {
    string blockName = 1;
    repeated string keys = 2;
}
```
Сообщение для запроса множества значений по нескольким ключам и блоку.

#### `TMordaGreenboxGetBulkResponse` {#TMordaGreenboxGetBulkResponse}
```proto
message TMordaGreenboxGetBulkResponse {
    map<string, string> result = 1;
}

```
Ответное сообщение для запроса множества ключей.
В ответе на [`TMordaGreenboxGetBulkRequest`](#TMordaGreenboxGetBulkRequest) содержит значение для каждого запрошенного ключа (пустую строку, если значения в хранилище не оказалось).

#### `TMordaGreenboxGetFirstOfBulkRequest` {#TMordaGreenboxGetFirstOfBulkRequest}
```proto
message KeyList {
    repeated string keys = 1;
}

message TMordaGreenboxGetFirstOfBulkRequest {
    string blockName = 1;
    repeated KeyList firstOf = 2;
}
```
Сообщение для запроса множества значений по нескольким спискам ключей и блоку. Для каждого списка ключей из запроса в ответе будет первый из списка ключ, для которого нашлось значение в хранилище. Если ни один ключ из списка не нашелся в хранилище, значения (даже пустой строки) для этого списка в ответе не будет. Ответ пишется в [`TMordaGreenboxGetBulkResponse`](#TMordaGreenboxGetBulkResponse)

### Обработчики

#### `/ping`
Отвечает стандартным `THttpResponse` с кодом 200 и телом `ok`

#### `/get`
Запрос одного ключа
Принимает `greenbox_get_request` типа [`TMordaGreenboxGetRequest`](#TMordaGreenboxGetRequest)
Возвращает `greenbox_get_response` типа [`TMordaGreenboxGetResponse`](#TMordaGreenboxGetResponse)

#### `/get_bulk`
Запрос множества ключей из одного блока
Принимает `greenbox_get_bulk_request` типа [`TMordaGreenboxGetBulkRequest`](#TMordaGreenboxGetBulkRequest)
Возвращает `greenbox_get_bulk_response` типа [`TMordaGreenboxGetBulkResponse`](#TMordaGreenboxGetBulkResponse)

#### `/get_first_of_bulk`
Запрос множества ключей из одного блока, в запросе передаются списки, для каждого списка будет отдано одно значение, если хотя бы для одного ключа из списка значение в хранилище нашлось, при этом из всех таких ключей будет выбран тот, который встретился первым в списке. Если ни одного ключа не нашлось значения, то значения для соответствующего списка в ответе не будет.
Принимает `greenbox_get_first_of_bulk_request` типа [`TMordaGreenboxGetFirstOfBulkRequest`](#TMordaGreenboxGetFirstOfBulkRequest)
Возвращает `greenbox_get_bulk_response` типа [`TMordaGreenboxGetBulkResponse`](#TMordaGreenboxGetBulkResponse)

## **bicycle_matrix HTTP API**

<br/>

## GET /v2/matrix

| параметр запроса | тип/формат/допустимые значения | описание |
|---|---|---|
| srcll | lon1,lat1~lon2,lat2~...lonN,latN | массив source точек |
| dstll | lon1,lat1~lon2,lat2~...lonN,latN | массив destination точек |

| заголовок запроса |
|---|
| **Accept**:</br>\*/\* (по умолчанию)</br>text/\* (для отладки) |

| код ответа  | тело ответа | заголовок ответа |
|---|---|---|
| 200 | proto-объект [Matrix](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bicycle_matrix/matrix.proto) | **Content-Type**    :</br>application/x-protobuf</br>text/x-protobuf |
| 400 | причина неудачи обработки запроса | **Content-Type**:</br>text/plain |

Matrix size is currently limited by 100 cells.
An error will be returned if srcll.size() * dstll.size() > 100

<br/>

## Asynchronous API

Пример использования: [тестовая стрелялка](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/matrix/shooter/lib/shooter.py?rev=r8196825#L80)

### POST /v2/matrix_stream/request

| заголовок запроса |
|---|
| **Accept**: application/octet-stream |
| **Content-Type**: application/x-protobuf |

| тело запроса |
|---|
| proto-объект [Request](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bicycle_matrix/request.proto) | application/x-protobuf |

| код ответа | тело ответа | заголовок ответа |
|---|---|---|
| 200 | pb stream proto-объектов [Row](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bicycle_matrix/matrix_stream.proto) | **Content-Type**:</br>application/octet-stream |
| 201 | Сервер начал обработку запроса. В следующий раз нужно идти по относительному пути GET <Location> | **Location**: ... |
| 400 | Ошибка клиента. Такой запрос повторять бесполезно | **Content-Type**:</br>text/plain |
| 500 | Ошибка сервера. Имеет смысл сделать перезапрос | **Content-Type**:</br>text/plain |

<br/>

### GET /v2/matrix_stream/status

| параметр запроса | тип/формат/допустимые значения | описание |
|---|---|---|
| token | string | Идентификатор асинхронного запроса, полученный в /v2/matrix_stream/request |

| код ответа  | комментарий | заголовок ответа |
|---|---|---|
| 202 | Запрос в процессе обработки, следует повторить запрос на данную ручку спустя <Retry-After> секунд | **Retry-After**:<seconds> |
| 308 | Результат вычислений готов, можно скачать по адресу <Location> | **Location**: URL файла pb stream proto-объектов [Row](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bicycle_matrix/matrix_stream.proto) |
| 404 | Задача не найдена, следует повторить оригинальный запрос /v2/matrix_steam/request | **Content-Type**:</br>text/plain |
| 410 | Ошибка сервера во время вычислений, следует повторить оригинальный запрос /v2/matrix_steam/request | **Content-Type**:</br>text/plain |
| 500 | Ошибка сервера при обработке запроса, следует повторить запрос на данную ручку | **Content-Type**:</br>text/plain |


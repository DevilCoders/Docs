## **HTTP API**

</br>

## GET /v2/matrix

| параметр запроса | тип/формат/допустимые значения | описание |
|---|---|---|
| srcll | lon1,lat1~lon2,lat2~...lonN,latN | массив source точек |
| dstll | lon1,lat1~lon2,lat2~...lonN,latN | массив destination точек |
| dtm | uint32 | время отправления в unixtime, по умолчанию текущее время |
| avoid | tolls | для построения матриц по бесплатным маршрутам, по умолчанию маршруты могут быть платными |
| vehicle_type | car, taxi или truck | тип ТС, по умолчанию car |
| vehicle_weight | float | вес ТС, тонны, по умолчанию не учитывается |
| vehicle_max_weight | float | макс. вес ТС, тонны, по умолчанию не учитывается |
| vehicle_axle_weight | float | нагрузка на ось, тонны, по умолчанию не учитывается |
| vehicle_payload | float | загрузка ТС, тонны, по умолчанию не учитывается |
| vehicle_length | float | длина ТС, метры, по умолчанию не учитывается |
| vehicle_height | float | высота ТС, метры, по умолчанию не учитывается |
| vehicle_width | float | ширина ТС, метры, по умолчанию не учитывается |
| vehicle_eco_class | 1, 2, 3, 4, 5 или 6 | эко-класс ТС, от 1 до 6, по умолчанию не учитывается |
| vehicle_has_trailer | true или false | есть ли прицеп у ТС, по умолчанию не учитывается |
| lang | код языка | код языка, для которого будут заполнены локализованные значения |

| заголовок запроса |
|---|
| **Accept**:</br>application/x-protobuf (по умолчанию)</br>text/x-protobuf |

| код ответа  | тело ответа | заголовок ответа |
|---|---|---|
| 200 | proto-объект [Matrix](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/driving_matrix/matrix.proto) | **Content-Type**:</br>application/x-protobuf</br>text/x-protobuf |
| 400 | Описание проблемы с переданными параметрами | **Content-Type**:</br>text/plain |
| 500 | Ошибка сервера при обработке запроса, следует повторить запрос на данную ручку | **Content-Type**:</br>text/plain |

</br>

## POST /v2/matrix_stream/request

| параметр запроса | тип/формат/допустимые значения | описание |
|---|---|---|
| dtm | uint32 | время отправления в unixtime, по умолчанию текущее время |
| avoid | tolls | для построения матриц по бесплатным маршрутам, по умолчанию маршруты могут быть платными |
| vehicle_type | car, taxi или truck | тип ТС, по умолчанию car |
| vehicle_weight | float | вес ТС, тонны, по умолчанию не учитывается |
| vehicle_max_weight | float | макс. вес ТС, тонны, по умолчанию не учитывается |
| vehicle_axle_weight | float | нагрузка на ось, тонны, по умолчанию не учитывается |
| vehicle_payload | float | загрузка ТС, тонны, по умолчанию не учитывается |
| vehicle_length | float | длина ТС, метры, по умолчанию не учитывается |
| vehicle_height | float | высота ТС, метры, по умолчанию не учитывается |
| vehicle_width | float | ширина ТС, метры, по умолчанию не учитывается |
| vehicle_eco_class | 1, 2, 3, 4, 5 или 6 | эко-класс ТС, от 1 до 6, по умолчанию не учитывается |
| vehicle_has_trailer | true или false | есть ли прицеп у ТС, по умолчанию не учитывается |

| заголовок запроса |
|---|
| **Accept**: application/octet-stream |
| **Content-Type**: application/x-protobuf |

| тело запроса |
|---|
| proto-объект [Request](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/driving_matrix/request.proto) | application/x-protobuf |

| код ответа | тело ответа | заголовок ответа |
|---|---|---|
| 200 | pb stream proto-объектов [Row](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/driving_matrix/matrix_stream.proto) | **Content-Type**:</br>application/octet-stream |
| 201 | Сервер начал обработку запроса. В следующий раз нужно идти по относительному пути GET <Location> | **Location**: ... |
| 400 | Ошибка клиента. Такой запрос повторять бесполезно | **Content-Type**:</br>text/plain |
| 500 | Ошибка сервера. Имеет смысл сделать перезапрос | **Content-Type**:</br>text/plain |

</br>

## GET /v2/matrix_stream/status

| код ответа  | комментарий | заголовок ответа |
|---|---|---|
| 202 | Запрос в процессе обработки, следует повторить запрос на данную ручку спустя <Retry-After> секунд | **Retry-After**:<seconds> |
| 308 | Результат вычислений готов, можно скачать по адресу <Location> | **Location**: URL файла pb stream proto-объектов [Row](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/driving_matrix/matrix_stream.proto) |
| 400 | Ошибка клиента, следует повторить оригинальный запрос v2/matrix_steam/request | **Content-Type**:</br>text/plain |
| 404 | Задача не найдена, следует повторить оригинальный запрос v2/matrix_steam/request | **Content-Type**:</br>text/plain |
| 410 | Ошибка сервера во время вычислений, следует повторить оригинальный запрос v2/matrix_steam/request | **Content-Type**:</br>text/plain |
| 500 | Ошибка сервера при обработке запроса, следует повторить запрос на данную ручку | **Content-Type**:</br>text/plain |

Результат вычислений доступен для скачивания в течение 10 минут.

## **matcher HTTP API**


</br>

## POST /matcher/v2/match_signals

| параметр запроса | тип/формат/допустимые значения | описание |
|---|---|---|

| заголовок запроса | тело запроса |
|---|
| **Accept**:</br>\*/\* (по умолчанию)</br>text/\* (для отладки) | proto-объект [SignalSequence](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/matcher/matched_path2.proto) |
| код ответа  | тело ответа | заголовок ответа |
|---|---|---|
| 200 | proto-объект [MatchedPath](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/matcher/matched_path2.proto) | **Content-Type**    :</br>application/x-protobuf</br>text/x-protobuf |
| 400 | причина неудачи обработки запроса | **Content-Type**:</br>text/plain |



## POST /matcher/v2/append_signals

В этом режиме использования сохраняется история сигналов по каждому UUID.
При вызове append_signals в историю добавляются новые сигналы и возвращается новый
маршрут от первого до последнего сигнала.
История хранится указанное в параметре ttl секунд с момента последнего вызова. (После каждого вызова счетчик ttl сбрасывается)

Для сброса истории достаточно вызвать append_signals с ttl = 0 (SignalSequence в этом случае может быть пустым).

Размер хранимой истории для одного uuid не может быть больше, чем 100 000 сигналов (чуть больше 1 суток при частоте сигналов раз в секунду).
При превышении этого объема, старые сигналы будут удаляться.


| параметр запроса | тип/формат/допустимые значения | описание |
|---|---|---|
| uuid | string | идентификатор пользователя |
| ttl | int | Время секундах хранения сигналов для uuid. |
| заголовок запроса | тело запроса |
|---|
| **Accept**:</br>\*/\* (по умолчанию)</br>text/\* (для отладки) | proto-объект [SignalSequence](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/matcher/matched_path2.proto) |
| код ответа  | тело ответа | заголовок ответа |
|---|---|---|
| 200 | proto-объект [MatchedPath](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/matcher/matched_path2.proto) | **Content-Type**    :</br>application/x-protobuf</br>text/x-protobuf |
| 400 | причина неудачи обработки запроса | **Content-Type**:</br>text/plain |

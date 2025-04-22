# История изменений

Все операции со справочникам шлются в [брокер](https://docs.yandex-team.ru/classifieds-infra/broker/info) в формате [MutationEvent](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/palma/event/dictionary_event.proto#L177):
* имя справочника
* идентификатор сущности
* старую сущность (one_of от моделей справочников)
* новую сущность (one_of от моделей справочников)
* кто поменял
* наименование сервиса
* requestId (Jaeger)
* когда поменял

Для шифрованных справочников не заполняется контент до и после мутации (Diff).

Из брокера данные попадают в
* YT [test](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/test/warehouse/palma/changelog/dictionary/1m) и [prod](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/palma/changelog/dictionary/1m)
* Kafka (топик `broker-palma-changelog-dictionary`)

## Гарантии
Честных гарантий нет.
После успешного создания/обновления/удаления сущности пытаемся логировать в брокер.
Если с нескольких попыток не получилось - логируем и метерим ошибку.

# geosearch-client - клиент для внутреннего API Яндекс.Карт

### Документация
https://wiki.yandex-team.ru/hevil/maps/api/geosearch/

### Краткая информация
Работает по протоколу protobuf.
Посмотреть обьекты которые  могут быть в ответе можно тут
https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto
Обьект верхнего уровня Response
https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto
Состав объектов внутри зависит от переданных параметров.

Если вам нужно получить параметры которых сейчас не хватает
1) Делаем запрос, видим что у части полей вместо названий числа.
2) Выбираем число которое заменяет название всей структуры.
3) Тут https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto
    ищем обьект в котором есть структура с таким id'шником, название будет вида RESPONSE_METADATA
4) В GeosearchResponseConverter.getRegistry добавляем запись вида
    registry.add(Geocoder.rESPONSEMETADATA);
    Эта записть добавляет в Response расширение в виде объекта Geocoder, rESPONSEMETADATA ссылка на расширение


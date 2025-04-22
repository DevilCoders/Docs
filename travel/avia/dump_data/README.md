Выгрузка справочников
=====================

Используется таской (arcadia/sandbox/projects/avia/dump_data)
для выгрузки справочников. Работает по принципу:
- для каждой таблицы в базе есть описание (arcadia/travel/avia/dump_data/lib/model_declaration.py)
- грузим данные из базы
- сериализуем с помощью protobuf (файлы .proto например arcadia/travel/proto/dicts/avia/company.proto)
- пишем в файл

Добавить новый справочник: (см. arcadia/sandbox/projects/avia/dump_data/README.md)

Парсинг crypta_id по идентификатору
===
Command-line утилита, которая возвращает все найденные crypta_id, и тип вершины для которой он был найден с нормализованной версией входящего  идентификатора.
Поддерживаются типы идентификаторов перечисленные [здесь](https://a.yandex-team.ru/arc_vcs/crypta/lib/native/identifiers/lib/id_types/all.h?rev=r8061831#L158-217).
Работает только с ascii символами!

### Запуск
```bash
# локально определяем переменную окружения
# открой https://yql.yandex-team.ru/oauth для получения токена
$ YQL_TOKEN='<your token>' 

# сборка
$ cd arcadia/crypta/graph/guess_identifier
$ ya make -r

# запуск
$ ./guess_identifier --id '<your id>'
```

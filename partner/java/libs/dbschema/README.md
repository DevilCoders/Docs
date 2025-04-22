Для получения свежей схемы и данных
- зайти на бету
- выполнить цель

```make generate_sql_for_java```

---
Цель запустит скрипт
```
./bin/generate_sql_for_java.sh
```
и выведет команды для синка sql и генерации jooq классов

1. Копирование sql
```
rsync -vaP --delete dev-partner2.sas.yp-c.yandex.net:/home/<username>/beta.<port>/java-dbschema/ src/main/resources/partner/
```

2. Создание jooq-классов
```
cd ../../dbschemagen
./update_jooq.sh
```

Подробная информация о скрипте [в README пакета dbschemagen](https://a.yandex-team.ru/arc/trunk/arcadia/partner/java/dbschemagen).

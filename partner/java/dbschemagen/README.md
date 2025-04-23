### Скрипт для обновления схемы БД ПИ

Использование:
```
./update_jooq.sh
```

Перегенерит классы в пакете libs/dbschema исходя из sql, которые лежат в его ресурсах


```
./update_jooq.sh --create-image
```

Перегенерит классы и создаст docker image с базой. Название образа запишется в
[dbschema_docker_image.txt](https://a.yandex-team.ru/arc/trunk/arcadia/partner/java/libs/test-db/src/main/resources/ru/yandex/partner/test/db/dbschema_docker_image.txt).
Использовать, если нужно обновить данные, участвующие в тестах, к которым не подключен MySQLRefresherService. Работать эти тесты будут только локально в Idea.

```
./update_jooq.sh --force-update
```

Перегенерит классы и создаст docker image с базой. Загрузит образ в registry, а так же ресурс с данными в sandbox.
Название образа запишется в
[dbschema_docker_image.txt](https://a.yandex-team.ru/arc/trunk/arcadia/partner/java/libs/test-db/src/main/resources/ru/yandex/partner/test/db/dbschema_docker_image.txt),
ID sandbox-ресурса - в [mysql-data.inc](https://a.yandex-team.ru/arc/trunk/arcadia/partner/java/libs/test-db/mysql-data.inc).
Использовать для того, чтобы тесты, к которым не подключен MySQLRefresherService, работали везде. Желательно выполнять
один раз, перед коммитом.

```
./update_jooq.sh --force-upload --force-mysql-server-upload
```

Дополнительно обновляет sandbox-ресурс с самой БД. Может пригодиться, если поменяется версия MySQL (?).



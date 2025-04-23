Локальный запуск
------
1. Копируем стабовые проперти
Создать `application-local.properties` из `application-local.properties.dist` в той же папке
Также `utilizer-vault-secrets.properties` из `utilizer-vault-secrets.properties.dist` в той же папке

2. Поднимаем докер контейнеры.
`cd 'dependency-stubs' && docker-compose up -d`.

3. Выполнить миграции
Необходимо будет указать путь до postgresql-42.2.5.jar
`liquibase --url=jdbc:postgresql://localhost:15800/utilizer \
--driver=org.postgresql.Driver \
--username=utilizer \
--password="utilizer" \
--changeLogFile=changelog.xml \
--classpath=postgresql-42.2.5.jar \
update`

4. Запустить приложение из IDE со следущими параметрами:

VM options:
```
-Denvironment=development
-Dspring.profiles.active=development
-Dlog.dir=logs
-Dconfigs.path=/src/main/properties.d
```
Для `-Dconfigs.path` можно указать абсолютный путь до `properties.d`

Для профиля `development` TMS задачи не будут запускаться автоматически.

Подробности в [описании фреймворка](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2).

Локальный запуск
------
1. Поднимаем докер контейнеры.
   `cd 'dependency-stubs' && docker-compose up -d`.

2. Выполнить миграции из папки /src/liquibase
   Необходимо будет указать путь до postgresql-42.2.5.jar
   `liquibase --url=jdbc:postgresql://localhost:15801/calendaring_service \
   --driver=org.postgresql.Driver \
   --username=calendaring_service \
   --password="calendaring_service" \
   --changeLogFile=changelog.xml \
   --classpath=postgresql-42.2.5.jar \
   update`

3. Запустить приложение из IDE со следущими параметрами:

VM options:
```
-Denvironment=development
-Dspring.profiles.active=development
-Dlog.dir=logs
-Dconfigs.path={абсолютный путь до папки properties.d}
```

Для профиля `development` TMS задачи не будут запускаться автоматически.
Подробности в [описании фреймворка](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2).

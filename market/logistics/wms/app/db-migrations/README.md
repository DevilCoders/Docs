# DB-MIGRATIONS

Проект включает в себя mssql миграция для проекта WMS.

## Локальный запуск и тестирования

Для тестирования миграции можно запустить локально:

`./check_migrations.sh`

При этом запустится база в docker, скачаются секреты в 
/etc/yandex/datasources/infor/application.properties и запустятся миграции.

После прогона миграций базу данных можно потушить командой:

`docker-compose down`

## Проблемы

`Warn: Failed to get token: No SSH keys found`

Решение: нужно добавить ssh ключ командой

`ssh-add ~/.ssh/*`


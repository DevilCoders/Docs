# Robot Result Storage Service

Сервис хранения, обработки и выдачи информации о результатах работы робота.

Документация в формате Swagger представлена в `docs/swagger.yml`

## Развёртывание

### Настройка `PSQL`

```postgresql
CREATE DATABASE rrs_db
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    CONNECTION LIMIT = -1;
```

### Как запустить

```shell
ya make
./bin/robot_result_storage_app alembic upgrade head
./bin/robot_result_storage_app
```

После запуска - http://127.0.0.1:81/docs - здесь можно посмотреть сгенерированную документацию и прототип API


### Миграции
В случае изменения модели
```shell
./bin/robot_result_storage_app alembic revision --autogenerate -m "Название"
```

Для обновления миграций:
```shell
./bin/robot_result_storage_app alembic upgrade head
```

# yeah

Грелка 2.0

## Работа в dev

### Создание БД

```
sudo su - postgres
psql
```

```
CREATE USER olegpro WITH password 'password';
CREATE DATABASE yeah OWNER olegpro ENCODING = 'UTF-8' lc_collate = 'en_US.utf8' lc_ctype = 'en_US.utf8' template template0;
GRANT ALL privileges ON DATABASE yeah TO olegpro;
SET client_encoding = 'UTF8';
```

Создание миграции

```
./tools/run-dev-alembic.sh revision --autogenerate -m "Migration slug"
```

Миграция
```
./tools/run-dev-alembic.sh upgrade head
```

### Запуск

```
./tools/run-dev-api.sh
./tools/run-dev-celery.sh
```

### Ручная сборка докера

```
$ ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/yeah/pkg.json
```

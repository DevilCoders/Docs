## Make migration
```
$ docker-compose run backend bash
# alembic revision -m "create test table"
```

## apply migration
```
# alembic upgrade head
```

## Окружения
Тестинг - https://deploy.yandex-team.ru/stages/tools_staff-dwh_testing
Прод - https://deploy.yandex-team.ru/stages/tools_staff-dwh_production

## Кластер psql в облаке
Тестинг
  - https://yc.yandex-team.ru/folders/foos73r5joh12svtcore/managed-postgresql/cluster/mdbp2nmt6038rts4ukih
  - БД staffdwh https://yc.yandex-team.ru/folders/foos73r5joh12svtcore/managed-postgresql/cluster/mdbp2nmt6038rts4ukih?section=databases

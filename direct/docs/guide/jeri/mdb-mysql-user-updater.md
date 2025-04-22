# Обновление настроек и пользователей MySQL в MDB (mdb-mysql-user-updater)

## О назначении программы { #about }


### Алгоритм действий

1. Счекаутить дирректорию <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/sync-db/conf-direct/etc/sync-db>
2. Счекаутить дирректорию <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mdb-mysql-user-updater>
3. Зайти в mdb-mysql-user-updater и собрать бинарник ya make
4. Взять ключ mdb_robot-direct-admin-manager из yav или /etc/direct-token
5. Запустить mdb-mysql-user-updater для нужного кластера.
```
./mdb-mysql-user-updater -command update-users -mdb-key /home/dspushkin/mdb_robot-direct-admin-manager  -grants-file ../sync-db/direct-production-mysql-grants.yaml -cluster-name ppcdata12-production
```

### Ссылки { #links }

- mdb-mysql-user-updater: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mdb-mysql-user-updater>

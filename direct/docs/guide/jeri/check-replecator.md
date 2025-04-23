# Проверка работы репликатора (replicator-check)

## О назначении программы { #about }

Программа replicator-check проверяет работу репликатора. На основе полученного списка гененрирует INSERT запросы в recomendation_status и вычитывает эту таблицу в YT.

### Алгоритм действий

1.На сервере может не оказаться нужных ключей, в зависимости от среды их требуется взять либо с ppcback, либо ppcdev.
2. счекаутить hostlist <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/hostlist>
3. собрать `ya make --checkout`
4. получить список реплик в шардах.
```
./hostlist -filter -production  -mdb-key /etc/direct-token/mdb_robot-direct-admin-viewer --json | cat > ./replicas-plan
или
./hostlist -filter -testing-2020  -mdb-key /etc/direct-token/mdb_robot-direct-admin-viewer --json | cat > ./replicas-plan
```
5. счекаутить replicator-check <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/dt-db-manager/cmd/replicator-check/main.go> 
6. собрать `ya make --checkout`
7. запустить проверку
```
./treplicator-check -cluster-restore zeno -account direct -directory-restore //home/direct/test/mysql-sync/dev7  -yt-token /etc/direct-tokens/yt_robot-direct-yt-test -mysql-token /etc/direct-tokens/mysql_direct-test -mysql-user direct-test -instances-file ./replicas-plan
```

### Мониторинг
<https://juggler.yandex-team.ru/check_details/?host=direct.prod_direct_ptkill_production&service=direct-mysql-ptkill-production&query=&last=1DAY>

### Ссылки { #links }

- replicator-check: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/dt-db-manager/cmd/replicator-check>
- hostlist: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/hostlist>

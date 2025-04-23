# Переключение MDB MySQL базы (mysql-change-master)

## О назначении программы { #about }

Программа создана для более простого переключения БД Директа из консоли.

### Алгоритм действий

1. заходим на ppcback машину, например на ppcback01f.yandex.ru
2. выполняем команду mysql-change-master с указанием имени кластера. В ходе работы программа предложит выбрать новый мастер.
```
/usr/local/bin/mysql-change-master -cluster-name ppcdata1-devtest
choose number host to master switch
1: sas-uwzwqdkmqu1a25qd.db.yandex.net (role: MASTER, alive: ALIVE)
2: vla-4d52oq0dd01kq9cn.db.yandex.net (role: REPLICA, alive: ALIVE)
2
2021-07-19:09:28:29.458900184 ppcback01f,direct.back/mysql-change-master,0:0:0 start switch master to sas-uwzwqdkmqu1a25qd.db.yandex.net -> vla-4d52oq0dd01kq9cn.db.yandex.net
2021-07-19:09:28:34.797589096 ppcback01f,direct.back/mysql-change-master,0:0:0 operation mdbdjsomujiboa6bfh6l progress
2021-07-19:09:28:39.752501706 ppcback01f,direct.back/mysql-change-master,0:0:0 operation mdbdjsomujiboa6bfh6l progress
2021-07-19:09:28:44.780217262 ppcback01f,direct.back/mysql-change-master,0:0:0 operation mdbdjsomujiboa6bfh6l done
```
3. переключение завершено, текущий мастер можно проверить через dbs-sql
```
dbs-sql dt:ppc:1 'select @@hostname'
```

Программу можно запустить в debug режиме и с возможностью прибивать старые запросы.
```
/usr/local/bin/mysql-change-master -cluster-name ppcdata1-devtest -debug
/usr/local/bin/mysql-change-master -cluster-name ppcdata1-devtest -kill
```

По умолчанию используется token находящийся в /etc/direct-tokens/mdb_robot-direct-admin-manager. Для запуска с другим токеном:
```
/usr/local/bin/mysql-change-master -cluster-name ppcdata1-devtest -token /tmp/newtoken
```

### Сборка
1. svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-change-master
2. cd mysql-change-master
3. ya package --debian pkg.json
4. tar -zxvf yandex-dt-mysql-change-master.<version>.tar.gz
5. dupload --to-direct-trusty yandex-dt-mysql-change-master_<version>_amd64.changes
6. переместить пакет stable и выложить на ppcback

### Пакет

Программа находится в пакете yandex-dt-mysql-change-master.

### Возможные ошибки

Если после выполнения запроса на смену мастера операция не выполняется, то возможно обновилась версия gRPC в MDB. Выглядеть может так:
```
dspushkin@ppcback01f:~$ /usr/local/bin/mysql-change-master -cluster-name ppcdata1-devtest
choose number host to master switch
1: sas-uwzwqdkmqu1a25qd.db.yandex.net (role: MASTER, alive: ALIVE)
2: vla-4d52oq0dd01kq9cn.db.yandex.net (role: REPLICA, alive: ALIVE)
2
2021-07-19:09:19:21.693379380 ppcback01f,direct.back/mysql-change-master,0:0:0 start switch master to sas-uwzwqdkmqu1a25qd.db.yandex.net -> vla-4d52oq0dd01kq9cn.db.yandex.net
dspushkin@ppcback01f:~$
```
Чтобы это исправить, надо пересобрать программу/пакет.

### Ссылки { #links }

- mysql-change-master: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-change-master>

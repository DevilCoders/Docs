## Как сгенерировать mysql таблички для канона?

### Найти сервер, где есть эти таблички

Например, bsmr-server02i.yandex.ru

### Уменьшить в размерах табличку MatrixNet

```bash
ilariia@bsmr-server02i:~$ sudo cp -r /var/lib/mysql.yabs/yabsdb/MatrixNet.MYI /var/lib/mysql.yabs/yabsdb/MatrixNet2.MYI
ilariia@bsmr-server02i:~$ sudo cp -r /var/lib/mysql.yabs/yabsdb/MatrixNet.MYD /var/lib/mysql.yabs/yabsdb/MatrixNet2.MYD
ilariia@bsmr-server02i:~$ sudo cp -r /var/lib/mysql.yabs/yabsdb/MatrixNet.frm /var/lib/mysql.yabs/yabsdb/MatrixNet2.frm
ilariia@bsmr-server02i:~$ sudo su
ilariia@bsmr-server02i:~$ su yabs
yabs@bsmr-server02i:/mnt/raid/home/ilariia$ mysql -uroot yabsdb
mysql> alter table MatrixNet2 drop column Data;
Query OK, 535 rows affected (0.67 sec)
Records: 535  Duplicates: 0  Warnings: 0
mysql> alter table MatrixNet2 drop column Dump;
Query OK, 535 rows affected (0.16 sec)
Records: 535  Duplicates: 0  Warnings: 0
```

### Загрузить все таблички в sandbox в папку mysql_tables
```bash
ilariia@bsmr-server02i:~$ mkdir t
ilariia@bsmr-server02i:~$ cp -r /var/lib/mysql.yabs/yabsdb/CTRPrediction.* t
ilariia@bsmr-server02i:~$ cp -r /var/lib/mysql.yabs/yabsdb/FormulaParameters.* t
ilariia@bsmr-server02i:~$ cp -r /var/lib/mysql.yabs/yabsdb/MatrixNet2.* t
ilariia@bsmr-server02i:~$ cp -r /var/lib/mysql.yabs/yabsdb/PageGroupExperiment.* t
ilariia@bsmr-server02i:~$ mv t/MatrixNet2.MYI t/MatrixNet.MYI
ilariia@bsmr-server02i:~$ mv t/MatrixNet2.MYD t/MatrixNet.MYD
ilariia@bsmr-server02i:~$ mv t/MatrixNet2.frm t/MatrixNet.frm
ilariia@ilariia-osx1:~$ mkdir mysql_tables
ilariia@ilariia-osx1:~$ mkdir mysql_tables/yabsdb
ilariia@ilariia-osx1:~$ scp -r bsmr-server02i.yandex.ru:~/t mysql_tables/yabsdb
ilariia@ilariia-osx1:~$ ya upload mysql_tables/ --ttl=inf -T AQINFRA_TESTS
Created resource id is 612732400
	TTL          : INF
	Resource link: https://sandbox.yandex-team.ru/resource/612732400/view
	Download link: https://proxy.sandbox.yandex-team.ru/612732400
```

### Заменить resource id в ya.make для тестов

```bash
sbr://612732400  # mysql tables
```

## Как сгенерировать matrixnet дампы для канона?

### Загрузить локально дамп из ресурса

Например, https://sandbox.yandex-team.ru/resource/276127353/view

### Загрузить дамп в тестовый ресурс

```bash
ilariia@ilariia-osx1:~/Downloads$ mkdir matrixnet_dumps
ilariia@ilariia-osx1:~/Downloads$ mv search_fresh_lol4_unstable_on_common_HLM40 matrixnet_dumps
ilariia@ilariia-osx1:~/Downloads$ ya upload matrixnet_dumps --ttl=inf -T AQINFRA_TESTS
Created resource id is 612937229
	TTL          : INF
	Resource link: https://sandbox.yandex-team.ru/resource/612937229/view
	Download link: https://proxy.sandbox.yandex-team.ru/612937229
```

### Заменить resource id в ya.make для тестов

```bash
sbr://612937229  # matrixnet_dumps
```

## Запустить тесты

```bash
ilariia@ml-dev:~/arcadia/ads/ml_monitoring/factors/ut$ ya make -t .
```

## Запустить c тестовым конфигом

```bash
ilariia@ml-dev:~/arcadia/ads/ml_monitoring/factors/bin$ MYSQL_PASSWORD=<password> GRAFANA_TOKEN=<token> ya make -r . && ./factors_dashboard  --conf-file ../resources/config_example.json  --mysql-user rplcat

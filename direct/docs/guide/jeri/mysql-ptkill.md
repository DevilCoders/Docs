# Прибивание старых запросов в MySQL (mysql-ptkill)

## О назначении программы { #about }

Программа mysql-ptkill2-master является доработкой pt-kill для возможности прибивания долгих запросов в БД MDB. Запускается по одному потоку для каждого шарда на ppcback машинах.

### Алгоритм действий

1. runit запускает mysql-ptkill2-master на ppcback* машинах(на каждой из машин работает по копии)
2. mysql-ptkill2-master вычитывает dbconfig и запускает по треду /usr/bin/pt-kill2 на каждый шард
3. mysql-ptkill2-master следит за текущими мастерами. Если мастер меняется, то запущенный тред с подключением к этой БД прибивается и стартует новый.
4. mysql-ptkill2-master пишет логи о прибитых запросах в /var/log/yandex/mysql-ptkill2.log. Лог отправляется в  logviewer: <https://direct.yandex.ru/logviewer/short/nDoVj6Ot42FeNC>
5. состояние работы mysql-ptkill2-master отправляется в juggler: <https://juggler.yandex-team.ru/check_details/?host=direct.prod_direct_ptkill_production&service=direct-mysql-ptkill-production&query=&last=1DAY>

В ps aux процесс выглядит так:
```
ppc       707479  0.0  0.0  47956 12728 ?        S    Jun17   3:24 python2 /usr/bin/mysql-ptkill2-master.py --dbconfig /etc/yandex-direct/db-config.json --log-file /var/log/yandex/mysql-ptkill2.log
ppc       707481  0.1  0.0 202736 52836 ?        S    Jun17  22:05 perl /usr/bin/pt-kill2 --host sas-a234kzl9ot9wo15d.db.yandex.net -D ppc --port 3306 --user ppc --password mSTWMNUiQplUHEu8qOq4 --filter /etc/ptkill/ppcdata.pl --busy-time 30 --ignore-command ^Sleep$ --kill-query --print --victims all --shard-name ppcdata11
ppc       707483  0.1  0.0 199728 49764 ?        S    Jun17  21:35 perl /usr/bin/pt-kill2 --host sas-tj0hzmcgju3e1b6r.db.yandex.net -D ppc --port 3306 --user ppc --password mSTWMNUiQplUHEu8qOq4 --filter /etc/ptkill/ppcdata.pl --busy-time 30 --ignore-command ^Sleep$ --kill-query --print --victims all --shard-name ppcdata13
...
```

### Запуск программы

Программа запускается через runit:
```
ppcback01f:# sv start /etc/sv/mysql-ptkill2-master
```
Пример запуска вручную:
```
/usr/bin/mysql-ptkill2-master.py --dbconfig /etc/yandex-direct/db-config.json --log-file /var/log/yandex/mysql-ptkill2.log
```

### Проверка работы

Чтобы проверить работу демона, нужно составить любой запрос больше 60 секунд с комментарием '/* pt-kill-me */'. Например:
```
HOST=vla-57yecmq4vp7h3fa3.db.yandex.net
mysql --default-character-set=utf8 --user=direct-sql --host=$HOST --port=3306 -p`cat /etc/direct-tokens/mysql_direct-sql` --comments ppc -e "select SLEEP(61), '/* pt-kill-me */'"
```

### Мониторинг
<https://juggler.yandex-team.ru/check_details/?host=direct.prod_direct_ptkill_production&service=direct-mysql-ptkill-production&query=&last=1DAY>

### Ссылки { #links }

- dt-mysql-ptkill2: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/mysql-ptkill2>

# Mysql binlog age check (mysql-binlog-age-check)

## О  программе { #about }

Программа проверяет самые старые по доступности позиции в mysql binlog и отправляет события о их возрасте в juggler.

### Алгоритм работы программы

1. При запуске программы берется блокировка в YT: hahn + locke(prod) / seneca-sas + locke(testing). Две блокировки гарантируют работу при поломке одного из кластеров YT. Запуск нескольких копий программы не критичен. Работа одним экземпляром носит эстетический характер и не создает лишних соединений с mysql.
2. Читает db-config из zookeeper и строит список хостов по шадам для подключения. Значения хостов для каждого шарда берется из 'hosts' db-config.
3. Для каждого мастера производится запуск отдельного потока(горутины), которая подключается к MySQL, вычитывает занятые server_id, назначает себе свободный из диапазона 6000-7000 и запускает репликацию.
4. Вычитавается первые 10 строк, чтобы получить дату первого event лога, после чего репликация останавливается.
5. При смене мастера в шарде, текущий поток останавливается, соединение с старым мастером закрывается и запускается поток с новым. 
5. Все проверки группируются по шардам и отправляются в juggler.

### Пример запуска программы
Варианты запуска прописаны в runsv скрипте mysql-binlog-age-monitor.sv: <https://arcadia.yandex.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-binlog-age-check/mysql-binlog-age-monitor.sv>

Ручной запуск(логи будут выводиться в syslog):
```
 export ZKPATH="/direct/np/db-config/db-config.test.json"
 export ENV="testing"
 export ZKSERVERS="ppc-zk-1.da.yandex.ru:2181,ppc-zk-2.da.yandex.ru:2181,ppc-zk-1.da.yandex.ru:2181"
 export YTLOCKPATH="//home/direct-np/apps/mysql-binlog-age-check/lock"
 export YTLOCKTOKEN="/etc/direct-tokens/yt_robot-direct-yt-test"
 export YTLOCKCLUSTER="locke,seneca-sas"
 /usr/local/bin/mysql-binlog-age-check -zkServers $ZKSERVERS -zkPath $ZKPATH -env $ENV -syslog -ytLockPath $YTLOCKPATH -ytLockCluster $YTLOCKCLUSTER -ytLockToken $YTLOCKTOKEN
```

Если не указывать syslog, то логи будут выводиться в stdout/stderr.

### Размещение
testing: <https://c.yandex-team.ru/groups/ppcdevs>
prod: <https://c.yandex-team.ru/groups/direct_backs>

### Сборка

Собрать можно из локальной копии на ноутбуке или ppcdev машине. 

```
 svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-binlog-age-check
 cd mysql-binlog-age-check
 ya package --debian pkg.json
 tar -zxvf yandex-mysql-binlog-age-check.1.8318098-1.tar.gz
    yandex-mysql-binlog-age-check_1.8318098-1_amd64.build
    yandex-mysql-binlog-age-check_1.8318098-1_amd64.changes
    yandex-mysql-binlog-age-check_1.8318098-1_amd64.deb
```

Отдельно бинарь можно собрать через ya make:
```
 cd mysql-binlog-age-check
 ya make
```

### Запуск/остановка

Версия для продакшена работает на ppcback*(condictor.direct_backs) серверах, для тестинга на ppcdevs*(conductor.ppcdevs). Запуск и остановку следует производить через runit:

```
 sv start /etc/sv/mysql-binlog-age-monitor
 sv stop /etc/sv/mysql-binlog-age-monitor
```

Программа не производит записей в БД или состояний работы в файлы. Останавливать можно TERM/KILL сигналы. 


### Мониторинг
При старте программы, запускается отдельный поток(горутина), которая отвечает за работу мониторинга. Она собирает значения времени самого первого binlog в шарде и на основе порогов отправляет событие в juggler:
5d - CRIT, 7d - WARN. Т.е. если первая запись event в binlog будет датирована 8 днями, то мониторинг будет зеленым, от 5 до 7 дней - желтым, меньше 5 - красным. Если логов не хватает меньше чем на 5 дней - это критичная ситуация, полная переливка баз YT будет невозможна.
<https://juggler.yandex-team.ru/check_details/?host=direct.prod_monitoring&service=mysql-binlog-age&query=&limit=200&last=1DAY> - aggregate production
<https://juggler.yandex-team.ru/raw_events/?query=service%3Dmysql-binlog-age-ppc1-production> - production/ppcdata1
<https://juggler.yandex-team.ru/raw_events/?query=service%3Dmysql-binlog-age-ppcdict-production> - production/ppcdict
<https://juggler.yandex-team.ru/raw_events/?query=service%3Dmysql-binlog-age-ppc1-testing> - testing/ppcdata1

### Диагностика
Прочитать вручную binlog можно посредством команды mysqlbinlog. Рассмотрим на примере с sas-zsv1rgyxg6dhaolw.db.yandex.net(команды с ppcback01f).
```
HOST=sas-zsv1rgyxg6dhaolw.db.yandex.net
mysql --host=$HOST --user=ppc --port=3306 -p`cat /etc/direct-tokens/mysql_ppc` -e 'SHOW MASTER LOGS' | head -2
берем самый первый лог из вывода и смотрим дату первых событий в нем
mysqlbinlog --host=sas-zsv1rgyxg6dhaolw.db.yandex.net --port=3306 --user direct-sql -p`cat /etc/direct-tokens/mysql_direct-sql` --read-from-remote-server mysql-bin-log-sas-zsv1rgyxg6dhaolw-db-yandex-net.001778 --base64-output=DECODE-ROWS -vvv | less
```

Если бинлогов недостаточно из-за переключений мастера, то это будет видно на графике `Disk usage on master` в YC:
* Зайти в <https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-mysql>
* Найти нужный кластер по шарду и окружению
* Во вкладке Monitoring есть `Disk usage on master`, а на графике отдельно `Used binlogs`

### Как чинить
В место под binlog имеет ограниченный размер и задается настройкой "Mdb preserve binlog bytes". 
1. Заходим в direct-infra/mysql: <https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-mysql>
2. Выбираем необходимый шард, например ppcdata16-production
3. Слева щелкаем по "Мониторинг" и смотрим на количество свободного места. 
4. Если free space остается меньше 300-400Гб, то перед увеличением следует добавить его: Обзор -> Изменить кастер(сверху справа) -> Увеличить размер хранилища.
5. Если свободного места достаточно, то накидываем ~100Гб: Обзор -> Изменить кластер -> Настройки СУДБ(внизу) -> Настроить -> добавить значение в Mdb preserve binlog bytes
6. Ждать заполнения логов в зависимости сколько дней не хватает. Если видно что лог заполнился, а проверка не погасла - следует повторить процедуру с увеличением значения.
 
Следует учитывать, что если на машине будет нехватать места, увеличение значения размера хранилища приведет к миграции контейнера на новую ноду(сервер). Это займет какое-то время, в течении которого с кластером сделать ничего не получится.

{% note warning "Другие причины алерта" %}

Алерт `mysql-binlog-age` чаще всего загорается из-за недостатка места для бинлогов. Однако, стоит иметь в виду, что бинлогов может быть недостаточно по другим причинам.

Пример: Из-за учений, нагрузки и т.д. произошло переключение мастера на реплику, которая не имеет достаточного количества бинлогов. В этом случае надо либо подождать необходимое количество дней, чтобы бинлоги догнались, либо вручную переключить мастера на реплику, где бинлогов достаточно.

{% endnote %}

### Логи
Логи работы записываются в /var/log/yandex/messages.log.<date> (например /var/log/yandex/messages.log.20210622).

### Ссылки { #links }

- Основной проект программы mysql-master-monitor: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-binlog-age-check>

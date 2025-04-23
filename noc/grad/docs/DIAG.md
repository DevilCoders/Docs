## Диагностика работы

### Нет данных
Проверяем что действительно нет данных, например посмотреть [solomon](https://solomon.yandex-team.ru/?project=noc&cluster=all&service=network&l.host=sas1-s10&l.ifname=all_interfaces&l.ifalias=-&graph=auto&l.sensor=rx).
Тут ссылка на service network в который приезжают данные сетевых счетчиков по SNMP. Если проблема с данным в другом сервисе, то нужно смотреть соответствующий сервис.
Дальше идем [сюда](https://monitoring.yandex-team.ru/projects/grad/dashboards/monb3f9onh8d0ra0tcip?range=1h&refresh=60&p.host=dante&p.poller=%2A) и смотрим график статусов опроса по каждому поллеру.
Если там что-то отличное от 1, то это значит что существует проблема со сбором. Например, таймауты.
Поле poller это инстанс поллера со своими набором SNMP OID или опросом через CLI.

### Проблемы со сбором SNMP
Первым делом нужно понять с какого сервера опрашивается хост. Это можно сделать выполнив c [продовых хостов](https://c.yandex-team.ru/groups/nocdev-grads):
```
sas-test-grads ~ $ get_cur_poller -d mnsk1-rp1
# fqdn grad сервер  | поллер       | хост, найденный по шаблону
sas1-grad2.yndx.net | SNMP freebsd | mnsk1-rp1
sas1-grad2.yndx.net | SNMP host resources storage#1 | mnsk1-rp1
sas1-grad2.yndx.net | SNMP linux cpu | mnsk1-rp1
sas1-grad2.yndx.net | SNMP snmp | mnsk1-rp1
```
get_cur_poller можно запустить с любого сервера [grad](https://racktables.yandex-team.ru/index.php?page=depot&tab=default&andor=and&cfe=%7B%24typeid_4%7D&cft[]=1594).
В выводе перечислены поллеры работающие с этим хостом и на каком сервере grad.
Дальше проверяем что хост вообще доступен с сервера grad и отвечает по SNMP:
```
sas-test-grads ~ $ snmpgetnext -v 2c -c znoc mnsk1-rp1 1
```
Если устройство не отвечает, то нужно проверить следующее:
- Фаерволл. https://puncher.yandex-team.ru/?destination=m9-6pe.yndx.net&rules=exclude_inactive&sort=source&source=_C_GRAD_
- Фаерволл2. Если хост в инете, то смотрим фаерволл на туннеляторах.
- Фаерволл3. У некоторых хостов есть локальный фаерволл, то надо обновить его и перезапустить.
- Фаерволл4. ACL на свитчах. Аннушкой запустить deploy -g snmp на этот хост.
- Настройки snmpd на Linux/FreeBSD. Поискать адрес града в /usr/local/etc/snmp/snmpd.conf или /etc/snmp/snmpd.conf.
- Настройки snmp на свитчах. Выкатить аннушкой.

Если отвечает на ```snmpgetnext 1```, но графиков всё еще нет, то нужно проверить ответ на oid'ы сетевых счетчиков.
Например, опросить 1.3.6.1.2.1.2.2.1.2(ifname). Если там
```
sas-test-grads ~ $ snmpwalk -v 2c -c znoc ivainfra-w17 1.3.6.1.2.1.2.2.1.2
iso.3.6.1.2.1.2.2.1.2 = No Such Object available on this agent at this OID
```
Такой вывод, то нужно проверить что разрешен опрос именно этих oid'ов.

Не лишним будет погрепать логи
```
grep man1-5s128 "/var/log/grad/SNMP freebsd.log"
```
Где имя файла совпадает с именем поллера.

Или посмотреть логи в [yql](https://yql.yandex-team.ru/Operations/YrrgPbq3kz5HFZt-DgmSkzkOjkH0BGOnjjt-wOecCtI=)

### Массовое сканирование доступности SNMP
С одного хоста проверить множество устройств:
```
snmp_pinger '{PDU} and not {$nameless}'
```
Проверить доступность одного устройства со всех градов:
```
executer p_exec %nocdev-grads 'snmpgetnext -v 2c -cznoc lab-vla-1s2 1 -r 1 -t 2 1>&- 2>&- && echo ok || echo timeout'
```
{% cut "про executer" %}

https://wiki.yandex-team.ru/users/serj0/executer/

Конфиг ~/.executer.conf:
```
qloud_disabled = 1
rtc_disabled = 1
project_filter=noc
```
{% endcut %}

### Дебаг grad-server
В каждом воркере есть обработчик сигнала USR1, который выведен много полезной информации через logger.

У grad-server есть несколько ручек:
http://server:12345/grad_server_debug - Статус в zookeeper, информация о задачах.\
http://server:12345/version - Версия сервера.\
http://server:12345/grad_server_all - Выгрузка всех хостов.

### Прочее
Вывода pcap'а в удобном виде:
```bash
tshark -2 -r /tmp/nsk6-s1.pcap -T fields -e frame.time -e _ws.col.Source -e _ws.col.Destination -e snmp.name -e snmp.request_id
# фильтр
tshark -2 -r /tmp/nsk6-s1.pcap -Y "snmp.name contains 1.3.6.1.2.1.2.2.1.2" -T fields -e frame.time -e frame.time_delta -e _ws.col.Source -e _ws.col.Destination -e snmp.max_repetitions -e snmp.name
```
Может пригодится для расследования. Например, в логах можно увидеть "CRITICAL - received after timeout reqid=52675". Можно погрепать дамп и найти запрос и ответ с этим id.
Есть скрипт для измерения частоты обновления данных.
```bash
# /usr/bin/get_update_freq -d 100 --community public localhost 1.3.6.1.2.1.2.2.1.16
oid                        min    avg    max
1.3.6.1.2.1.2.2.1.16.1     2.93   2.98   3.04
1.3.6.1.2.1.2.2.1.16.2     2.93   3.00   3.04

poll duration min=20.440981 max=21.053355 avg=20.888344
```
Скрипт первым шагом получается все OID'ы для указанного дерева, а дальше начинает их постоянно опрашивать и записывать даты смены значений.
Соответственно чем дольше опрашивает скрипт, тем точнее данные будут.
В последней строке указана статистика по длительности опроса.

## Вендорские дела
Получение данных на самом Huawei:
```bash
system-view
diagnose
display snmp-agent mib walk 1.3.6.1.4.1.2011.5.25.32.1.1.5
```

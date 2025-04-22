Цель проекта — получение и обработка данных с разнообразных устройств. Основной упор сделан на возможность обработки данных перед отправкой, так как часто получаемые данные далеки от идеала.

Схема:\
<img src="https://jing.yandex-team.ru/files/gescheit/Metridat%20%2B%20grad.jpg" alt="drawing" width="1000"/>

## Дашборды
[Дашборд](https://grafana.yandex-team.ru/d/000009488/grad?panelId=17&orgId=1&from=now-2d&to=now) \
[Дашборд](https://monitoring.yandex-team.ru/projects/grad/dashboards/monvk9vkojrkijuiu806?range=1d&refresh=60) \
[error booster](https://error.yandex-team.ru/projects/grad)

## Метрики
##### scheduler_status
сенсор | Описание
--- | ---
duration | Длительность выполнения Job

##### scheduler_status_value
сенсор | Описание
--- | ---
reason | Результат выполнения Job. Смотри [значения](https://a.yandex-team.ru/arc/trunk/arcadia/noc/grad/grad/lib/scheduler.py?rev=r9321280#L33)

##### scheduler
сенсор | Описание
--- | ---
job_delay | Разница между запланированным стартом и реальным началом выполнения.

##### scheduler_queues
сенсор | Описание
--- | ---
qsize | Загруженность очереди в сторону RMQ
qsize_lb | Загруженность очереди в сторону LogBroker
qdrop | Количество удаленных данных из очереди в сторону RMQ. Удаляется при переполнении
qdrop_lb | Количество удаленных данных из очереди в сторону LogBroker. Удаляется при переполнении
sent | Количество отосланных наборов данных. Обычно один Job возвращает 1 набор после выполнения.
sent_sensors | Количество отосланных сенсоров

##### scheduler_jobs
сенсор | Описание
--- | ---
run | Количество активных Job
total | Всего Job

##### function_duration
сенсор | Описание
--- | ---
duration | Длительность выполнения функция

##### function_duration
сенсор | Описание
--- | ---
duration | Длительность выполнения функция
##### import_external
сенсор | Описание
--- | ---
duration | Длительность выполнения импорта
error | Статус ошибка или нет

Графики по некоторым сенсорам:\
[scheduler_queues/qsize*](https://monitoring.yandex-team.ru/projects/grad/explorer/queries?q.0.s=%7Bproject%3D%22grad%22%2C%20cluster%3D%22vla%22%2C%20service%3D%22scheduler_queues%22%2C%20sensor%3D%22qsize%2A%22%7D&from=now-1h&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg) - загрузка очередей в сторону LB/RMQ.\
[scheduler_queues/sent_sensors](https://monitoring.yandex-team.ru/projects/grad/explorer/queries?q.0.s=non_negative_derivative%28%7Bproject%3D%22grad%22%2C%20cluster%3D%22vla%22%2C%20service%3D%22scheduler_queues%22%2C%20sensor%3D%22sent_sensors%22%7D%29&from=now-1d&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg) - количество отосланных данных.\
[scheduler_jobs/run|total](https://monitoring.yandex-team.ru/projects/grad/explorer/queries?q.0.s=%7Bproject%3D%22grad%22%2C%20cluster%3D%22vla%22%2C%20service%3D%22scheduler_jobs%22%2C%20sensor%3D%22run%7Ctotal%22%2C%20poller%3D%22SNMP%20Arista%20network_0%22%7D&from=now-1d&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg) - список задач активных и ожидающих.\
[scheduler_status_value/reason](https://monitoring.yandex-team.ru/projects/grad/explorer/queries?q.0.s=%7Bproject%3D%22grad%22%2C%20cluster%3D%22%2A%22%2C%20service%3D%22scheduler_status_value%22%2C%20thost%3D%22vla1-e1%22%2C%20poller%3D%22SNMP%20juniper%20per_queue_%2A%22%7D&from=now-1d&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg) - статус завершения задач.\
[import_external/duration](https://monitoring.yandex-team.ru/projects/grad/explorer/queries?q.0.s=%7Bproject%3D%22grad%22%2C%20cluster%3D%22%2A%22%2C%20service%3D%22import_external%22%2C%20sensor%3D%22duration%22%2C%20import_name%3D%22bot_data%22%2C%20res_type%3D%22%2A%22%7D&from=now-1d&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg) - длительность работы импортов из RT/Bot и прочих внешниих источников.

## Сборка и выкатка
В noc/grad/packages/ лежат настройки нескольких пакетов. Пример сборки руками grad_server:
```shell
ya packages noc/grad/packages/grad_server/pkg.json --debian
```

Сама же аркадия заливает пакеты в unstable и testing. В stable перенести можно так:
```shell
ssh noc.dupload.dist.yandex.ru
find_package -r noc -e testing grad-server | grep _amd64.deb
sudo dmove noc stable grad-server 1.8.xxx testing
```

Удаление старых пакетов:
```shell
ssh noc.dupload.dist.yandex.ru
sudo rmove noc stable grad-server 1.8.xxx
# из testing, unstable и stable
````

Массовое удаление старых пакетов:
```shell
find_package -r noc -e unstable grad-server | grep _amd64.deb | cut -d "|" -f 4 | cut -d "_" -f 2 | xargs -I VER sudo rmove noc testing grad-server VER
```
Выкатить продовый конфиг:
```shell
executer p_exec %nocdev-grads "salt-call state.highstate"
```

Выкатить пакет руками:
```shell
executer p_exec %nocdev-grads "apt-get update; apt-get install grad-server=1.8...."
executer p_exec %nocdev-grads "salt-call state.sls units.nocdev-grads"
```

## SLB и мониторинги
Для балансера есть ручка http://fqdn:12345/ping. Отвечает 200, если сервер захватил zookeeper лок и подключился к rmq.
Там же есть ручка /grad_server_info, в которой есть некоторая дебажная информация. В нее ходят проверки.

## RabbitMQ
Веб-интерфейс RabbitMQ доступен по ссылке http://fqdn:15672. Данные пишутся в exchange=grad_local.
И распределяются по нодам через federated exchange. Тут можно проверить что во вкладке Exchanges есть подключения к другим нодам.

Дебаг:
```shell
ngrep -d lo m9-s4 port 5672
```

[Графики](https://solomon.yandex-team.ru/?project=grad&cluster=all&service=rabbitmq_exchange&l.sensor=messages_publish_out&l.host=*&l.exchange=local_grad&graph=auto&transform=differentiate&stack=false&b=1d&e=) посылки данных в rmq.

Посмотреть на данные:
```
# ngrep -tq -d lo 'tunnel_ping' port 5672
```

## grad-server
Пишет логи в /var/log/grad/server.log /var/log/grad/server_pollers.log. Исключительные ситуации могут быть видны в `journalctl -f -u grad-server`. В списке процессов на мастер-хосте должно примерно это
```
root     19112  /usr/bin/grad_server -c /etc/grad/grad_server.yml --config-directory /etc/grad/conf.d [main server]
root     19415  /usr/bin/grad_server -c /etc/grad/grad_server.yml --config-directory /etc/grad/conf.d [poller SNMP cisco power]
root     19417  /usr/bin/grad_server -c /etc/grad/grad_server.yml --config-directory /etc/grad/conf.d [poller SNMP Ekinops_RM100_line]
root     19419  /usr/bin/grad_server -c /etc/grad/grad_server.yml --config-directory /etc/grad/conf.d [poller SNMP huawei_power]
root     19421  /usr/bin/grad_server -c /etc/grad/grad_server.yml --config-directory /etc/grad/conf.d [poller SNMP huawei total qos]
root     19423  /usr/bin/grad_server -c /etc/grad/grad_server.yml --config-directory /etc/grad/conf.d [poller SNMP freebsd]
...
```

# Данные
grad_server посылает данные в rabbitmq в exchange **grad_local** типа topic.
Есть скрипт utils/rmq_cat.py. Он может подключится к rmq и показывать данные.
Данные выглядят так:

routing key = snmp_poller.network
data = `[[1521111600, {'host': 'vla1-x5', 'ifname': 'et-7/0/9.0'}, {'rx_packets': 0, 'tx': 0, 'rx_errs': 0, 'flap': 0, 'rx': 0, 'rx_drop': 0, 'tx_unicast': 0, 'tx_errs': 0, 'speed': 100000, 'admin_status': 1, 'tx_nunicast': 0, 'rx_nunicast': 0, 'tx_packets': 0, 'rx_unicast': 0, 'tx_drop': 0}]]`
Данные упакованы в JSON в список `[[TS, keys, values], [TS, keys, values], ...]`.
routing_key, в случае snmp, состоит из константы snmp_poller и настраиваемой в конфиге переменной(series: network). Пример конфига:
```yml
  SNMP vmware:
    poller: snmp
    poller params:
      counters: *network_key_ifname
      post_fn: [check_net_data_stage1, sum_counters, check_net_data_sanity]
      skip_key_expr: '(vmk\d+)'  # заблокирован так как наблюдается глюк у уменьшением счетчика
    filter: "{телефонный сервер} and {VMware} and {гипервизор} and not ({$nameless} or {уже не работает})"
    series: network
    interval: 120
```

## Конфиг
Подробности про составление конфигов смотри в [разработка и тестирование](https://a.yandex-team.ru/arcadia/noc/grad/docs/README.TESTING.md).
Конфигурация сервера находится в [grad_server.yml и в директории conf.d](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-grads/files/etc/grad).

## Требования к устройствам
Для выполнения команд(таких как ethtool -S, vtysh, ...) на Linux через sudo есть пакет [monitor-sudoers](https://a.yandex-team.ru/arcadia/noc/packages/monitor-sudoers).

## Диагностика grad-server
 - Правим тестовый конфиг grad_server_test.yml
 - Запускаем сервер командой ```./grad_server --config grad_server_test.yml -l```
 - Получаем данные командой ```curl "http://127.0.0.1:12346/local_grad/#"```

Сервер будет писать логи в консоль из-за опции -l, иначе в указанные в конфиге файлы.
Нужно учесть что дырок может и не быть. Если используется comocutor'ный поллер, то нужно поправить credentials.yml.

Выполнение команды на всех серверах:
```bash
make print_servers | xargs -I HOST ssh HOST "grep retransmits.py /var/log/grad/main\ comocutor\ instance\#*.log | awk -F'Job\\\(' '{print \$2}' | cut -d ' ' -f 1" | sort -u
```
Информация о том какой сервер опрашивает хост:
```bash
# на grad'е
/usr/bin/get_cur_poller -d sas2-5s99
# в проекте
make HOST=sas2-5s99 get_cur_poller
```

### Доступы
Сервера град опрашивают с адресов из ```_GRAD_ALL_HOSTS_``` и ```_C_GRAD_```.\
Так как есть много хостов с IPv4 mgmt, то используется туннельная схема. Туннельные сети указаны в GRAD_ALL_HOSTS.
Где есть дырки:
- Дырки в панчере. Предзаполненная форма [puncher](https://puncher.yandex-team.ru/?create_comment=grad%20SNMP%20access&create_ports=161&create_protocol=udp&create_sources=_GRAD_ALL_HOSTS_,_C_GRAD_&create_until=persistent). Все дырки можно найти поискать по указанным выше макросам.
- Дырки в инет через туннеляторы в fw/sections/INET4ALL.
- SNMP ACL в [генераторе аннушке](https://noc-gitlab.yandex-team.ru/nocdev/annushka/-/blob/master/annushka/generators/snmp_acl.py).
- MGMT ACL(CLI/netconf) в [генераторе аннушке](https://noc-gitlab.yandex-team.ru/nocdev/annushka/-/blob/master/annushka/generators/mgmt_acl.py).
- Дырка до SNMP офисных серверов [как тут](https://st.yandex-team.ru/NOCRFCS-11545).
- На офисных серверах SNMP ACL конфиг в routers/conffiles/snmpd.conf и там же есть таргет для обновления.
- SNMPD на прочих(switchdev, cumulus, linux и некоторых FreeBSD) устройствах в [аннушке](https://noc-gitlab.yandex-team.ru/nocdev/annushka/-/blob/master/annushka/generators/entire/snmpd.py).
- Дырки на [голосовых шлюзах](https://st.yandex-team.ru/IPTEL-5099).
- Статичные правила для рефлекторов - https://noc-gitlab.yandex-team.ru/nocdev/annushka/-/merge_requests/4139/diffs.
- Для облака есть отдельный проверки откуда можно подключаться - SECALERTS-417818.

### Redis
Сброс данных:
```
redis-cli flushall
```

### grad client
[Дашборд с зедержками](https://grafana.yandex-team.ru/d/iyW_44fWz/grad-client-lateness?orgId=1)

### Как найти к какому серверу rabbitmq подключен потребитель?
```
executer p_exec %grad,-grad-dev.yndx.net "curl -s -u guest:guest http://localhost:15672/api/consumers | jq '.[] | select(.queue.name==\"federation.TT\" and .channel_details.user != \"federation\") | .channel_details'"
```

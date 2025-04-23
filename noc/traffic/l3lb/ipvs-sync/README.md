# Предпосылка создания ipvs-sync

Каждый из балансеров тратит достаточно большое количество CPU-ресурсов только на то, чтобы проверять доступность рилов; если сервис живет на нескольких соседних балансерах, то количество проверок per real увеличивается на количество балансеров.

Чтобы разгрузить балансеры возникла идея сделать некий мастер/арбитр, который будет заниматься исключительно проверками и доставлять эту информацию до приборов, задача которых балансировать трафик.

# Описание работы

ipvs-sync состоит из:

- [config.ini](#config.ini) — конфигурационный файл с набором переменных;
- [server](#server) — приложение, которое мониторит изменение дерева IPVS и доставляет данные в брокер очереди (в нашем случае rabbitmq);
- [client](#client) — обрабатывает сообщения от сервера и применяет их, также отправляет со своей стороны сообщения при необходимости синхронизации этих данных;
- [quorum-action](#quorum-action) —  является заменой /etc/keepalived/quorum-handler2.sh на серверной стороне.

Дерево IPVS строится с использованием netlink и отправкой/чтением событий в/из rabbitmq.  
Общая структура работы server и client частей представлена на [рисунке](https://github.yandex-team.ru/mnt-traf/ipvs-sync/blob/master/ipvs-sync.png).

## config.ini
[Чтение/сохранение mapping-а балансеров и IP-адресов сервисов.](#service_mapping_worker)

    mapping_update_interval = 60
    service_mapping_wildcard = /etc/keepalived/lbs/*/*/*.conf
    service_mapping_config = /var/tmp/svc_mapping.json
    export_service_mapping_wildcard_to_config = true

[Чтение файлов-состояния VIP-адресов.](#vips_description_worker)

    vips_description_update_interval = 0.5
    vip_description_filepath = /var/run/keepalived-*-desc.json

[Обновления состояния клиентов.](#active_consumers_worker)

    consumer_alive_ttl = 15
    active_consumers_update_interval = 0.1

[amqp_server = amqp://](#client_requests_worker)  
[announces_source = Client](#prepare_answer_worker)  

[Интервал клиентских запросов.](#client)

    heartbeat_interval = 3
    tree_request_interval = 120
    announces_request_interval = 300

[Дополнительные параметры клиентской части.](#announces_worker)

    announces_queue_limit = 524288
    firewall_update_try = 2


## server
[server.py](https://github.yandex-team.ru/mnt-traf/ipvs-sync/blob/master/server.py)  
При запуске серверной части в рамках main fork-ается также 7 процессов:

- [service_mapping_worker](#service_mapping_worker)
- [vips_description_worker](#vips_description_worker)
- [active_consumers_worker](#active_consumers_worker)
- [client_requests_worker](#client_requests_worker)
- [prepare_answer_worker](#prepare_answer_worker)
- [send_events_worker](#send_events_worker)
- multiprocessing.Manager()

Ниже каждый из процессов будет рассмотрен подробнее.  
Помимо создания указанных worker-ов также каждый цикл main:

- проверяет живость всех worker-ов и, в случае если один из них не alive, вызывает RuntimeError исключение;
- обновляет состояние IPVS-дерева пробует построить diff в предыдущим значением, если успешно — отправяет changes, если нет, то tree.  

Подготовленные для отправки данные добавляются в processing_queue.

Используемые очереди:
- client_requests_queue:
  - write: [client_requests_worker](#client_requests_worker);
  - read: [prepare_answer_worker](#prepare_answer_worker);
- processing_queue:
  - write: main, [prepare_answer_worker](#prepare_answer_worker);
  - read: [send_events_worker](#send_events_worker).

У каждой из очередей есть свое ограничение на количество сообщений в очереди, по наступлению которых запись в очередь становится блокируемой:

    client_requests_queue_limit = 262144
    processing_queue_limit = 65536

### service_mapping_worker
Процесс мониторит состояние mapping-а, то есть соответствия сервисов для каждого из балансеров,  
например: `{"myt-lb15a.yndx.net": ["2a02:6b8::2:105", "141.8.146.159", "141.8.146.138", "2a02:6b8::9"]}`.  
Почему вынесен в отдельный процесс: если в config.ini объявлена опция `export_service_mapping_wildcard_to_config`, то процесс пытается разобрать конфигурации в `service_mapping_wildcard`, а поскольку таких конфигураций очень много, это занимает существенное время на IO операции, а также CPU (каждая из конфигураций split-ится в поиска IP-адреса сервиса).  
Также конфигурацию можно читать из `service_mapping_config` или сохранять туда данные — всё зависит от выставленной опции экспорта, описанной выше.  
`mapping_update_interval` устанавливает sleep-интервал между чтениями файлов конфигураций.

### vips_description_worker
Собирает информацию о текущем состоянии анонсов VIP-адресов.  
Конфигурации читаются из `vip_description_filepath` и склеиваются в словарь вида `{"VIP": {"active": <int>, "announce": <bool>, "total": <int>, "local-preference": <int>}`.
Интервал обновления конфигурации устанавливается с помощью `vips_description_update_interval`.

### active_consumers_worker
Worker проверяет время последнего получения запроса heartbeat от клиента с интервалом `active_consumers_update_interval`. Если время последнего доступа превышает TTL = `consumer_alive_ttl`, то данный клиент удаляется из списка активных потребителей и ему перестает доставлять информация об изнении дерева.

### client_requests_worker
Основное назначение процесса: читать данные от клиентов на Exchange=ipvs с routing-kee=lbs и добавлять полученные от клиентов запросы в очередь client_requests_queue. Больше этот процесс ничего не делает.  
Использует переменную `amqp_server`, в которой описано как подключаться к AMQP брокеру очередей.

### prepare_answer_worker
Пожалуй наиболее функциональная часть серверной части:  
здесь, в зависимости от полученного запроса со стороны клиента, собираются данные с использованием shared namespace и формируется тело ответа. Логика включает в себя поиск функции (среди локальных) _func_<тип запроса> и передача функции тела запроса.  

Какие действия соответствуют своему типу запросов:
- tree: возвращает IPVS-дерево;
- services: возвращает IPVS-дерево для указанных в запросе VIP `{'ipaddrs': [VIP_1, VIP_2, ...]}`;
- mapping: возвращает содержимое services_mapping_per_balancer, подготовленное в [service_mapping_worker](#service_mapping_worker);
- sync: возвращает содержимое запрашиваемых файлов `{filename_1: data_1, filename_2: data_2}` для запроса с указанием `{filenames: [list files]}`, файлы умеет читать также по маске — внутри используется glob;
- announces: подготавливает IPVS-дерево для каждого VIP `{VIP1: {VIP1 tree}, VIP2: {VIP2 tree}}`, например, `{'5.255.240.50': { '2_5.255.240.50_80_TCP_wrr_0': [u'2_77.88.1.115_80_1_0_0_TUNNEL'], '2_5.255.240.50_443_TCP_wrr_0': [u'2_77.88.1.115_443_1_0_0_TUNNEL']}, }` и генерирует запрос syn_announce;
- syn_announce: возвращает payload;
- ack_announce: запрос со стороны клиента о том, что можно передавать анонс для данного VIP; внутри валидируется то, что для данного VIP состояние = {"announces": true}, а также то, что в services_mapping_per_balancer есть упоминание этого VIP для данного балансера и является ли данный хост "мастером", то есть установлено ли `announces_source = Server`;
- heartbeat: обновляет время получение сообщения в списке активных клиентов. Также если клиент был только добавлен в список, для него генерируются сообщения tree, mapping и announces.

Полученные тела ответа добавляются в очередь processing_queue.

### send_events_worker
Worker бесконечно читает очередь сообщений processing_queue и в рамках своего отдельного соединения с rabbitmq (на localhost) отправляет сообщения для клиентов.  
Сообщения могут быть 2 типов:
- unicast, когда указан 'destination', в этом случае сообщение оправляется как direct с routing_key = destination;
- multicast, используется когда не указан 'destination', но определен [services_mapping_per_balancer](#service_mapping_worker). В качестве получателей использует список активных клиентов.

Есть также возможность отправлять broadcast, но в серверной части эта функциональность не используется.


## client
[client.py](https://github.yandex-team.ru/mnt-traf/ipvs-sync/blob/master/client.py)

Основная задача приложения — процессинг сообщений со стороны сервера;  
для каждого из типов сообщений определены свои действия:

- tree, сверяет полученное дерево сообщений со своим состоянием и применяет его;
- changes, валидирует изменения и применяет их;
- mapping, обновляет дерево IPVS в соответствии с полученным состоянием и отправляет tree запрос в сторону клиента;
- sync, сохраняет файлы и их содержимое в соответствии со словарем `{filename_1: data_1, filename_2: data_2}`;
- execute, вызывает соответствующую команду, переданную в качестве аргумента;
- syn_announce, добавляет данные в очередь ANNOUNCES_QUEUE, которую в дальнейшем процессит announces_worker, представляет из себя сообжение вида `{vip_1: vip_ipvs_tree_1, vip_2: vip_ipvs_tree_2}`;
- fin_announce, удаляет переданный VIP с loopback интерфейса или вызывает `/etc/keepalived/quorum-handler2.sh down` — если `announces_source = Client` в config.ini;
- heartbeat, ничего не делает — действие-заглушка.

`announces_queue_limit` управляет размером очереди сообщений ANNOUNCES_QUEUE, и по аналогии с серверной частью: при достижении порогового значения запись в очередь становится блокируемой.  
Взаимодействует с данной очередью отдельный тред [thread announces_worker](#announces_worker), задач которого — проверка возможности поднятия анонса VIP-адреса.

Помимо этого, в соответствии с заданным интервалами обновления в config.ini, client отправляет запросы, которые препятствуют появлению рассинхнонизации:
- tree
- heartbeat
- announces

### announces_worker
Thread проверяет наличие правил в конфигурации файрвола `/etc/init.d/load-iptables.sh` и при необходимости обновляет список правил.  
Количество обновлений ограничено опцией `firewall_update_try`.  
Если VIP есть в списке правил файрвола, то принимается решение: "поднять адрес на loopback интерфейсе или вызвать `quorum-handler2.sh`?" — по аналогии с функцией fin_announce.  
Также применяется новое IPVS-дерево для сервисов, полученное из очереди ANNOUNCES_QUEUE.


## quorum-action
[quorum-action.py](https://github.yandex-team.ru/mnt-traf/ipvs-sync/blob/master/quorum-action.py)

Является заменой quorum-handler2.sh на серверной стороне.  
При вызове данного скрипта, например `quorum-action.py up 2a02:6b8::1:1,b-100,0`:

- читает и правит `vip_announces_filepath = /var/run/keepalived-%s-desc.json`:
    - пересчитывает значение активных портов и их общее количество, если оно изменилось — `{"active": 0, "total": 0}`;
    - меняет состояние announce на true, если active == total, иначе false.
- перечитывает состояние `service_mapping_config = /var/tmp/svc-mapping.json` и составляет из него список балансеров (destinations);
- если событие "down", то посылает withdraw сообщение в ExaBGP для каждого из балансеров в destinations, а также рассылает broadcast сообщение fin_announce;
- если событие "up", то генерирует сообщение в сторону каждого destinations вида `{'syn_announce': {vip: vip_data}}`.


# Тестирование
Для запуска тестов необходимо выполнить:

    $ cd modules
    $ python -mpytest tests/


# Сборка
Для того, чтобы собрать пакет, необходимо запустить:

    # make package

Если необходимо собрать только библотеку:

    $ make fetch extract build

# Подготовка к запуску
## Настройка мастера
1. синнхронизация тегов балансера (признак того, является ли балансер ipvs-sync-server или client хранится в тегах):

        # /opt/balancers/scripts/get-lb-tags.py

2. установка rabbitmq-сервер и пакета ipvs-sync

        # apt-get install rabbitmq-server=3.2.4-1ubuntu0.1 ipvs-sync

3. синхронизация файла с паролями с secdist и изменение прав доступа:

        # scp secdist.yandex.net:/repo/projects/mnt-traf/environment/ipvs-sync.ini /etc/ipvs-sync/secret.ini
        # chown monitor:root /etc/ipvs-sync/secret.ini
        # chmod 440 /etc/ipvs-sync/secret.ini

4. добавление пользователя под которым будут работать клиенты - команды указаны в файле /etc/ipvs-sync/secret.ini
5. удаление пользователя guest в rabbitmq:

        # rabbitmqctl delete_user guest

6. создание symlink quorum-handler.sh, который будет корректно процессить события quorum up/down,  
меняется логика обработки событий таким образом, что они начинабт доставляться в сторону клиентов

        # ln -sf /opt/venvs/ipvs-sync/bin/quorum-action.py /etc/keepalived/quorum-handler2.sh

7. удалить из конфигураций bird все dummy интерфейсы за исключением dummy0 и dummy255
8. заведение сервиса и применение правил файрвола (эту логику делает scripts/ifup-ipvs-sync-server, которых выполняется при поднятии dummy0)

        # ipvsadm -A -t 213.180.205.70:5627 -s wrr
        # ip addr add 213.180.205.70/32 dev dummy0
        $ sudo -E make -C /usr/local/balancers/iptables update install restart

## Настройка клиента
Пункты 1-3 аналогичны тем, что выполняются на стороне мастера.
После этого запускаем ipvs-sync-client и смотрим логи:

    # start ipvs-sync-client
    # tail -f /var/log/ipvs-sync.log

# Мониторинг
Компонент, помогающих следить за состоянием сервиса, две:
- monit
- juggler

Monit выполняет роль автоматического fallback-а и демона, следящего за наличием процессов,
настраивается это все в конфигурационном файле confs/monit/conf.d/monit-ipvs-sync-check.conf.
При неуспешном выпонении monitoring.py вызывается скрипт помощник monit-action.sh,
который в случае fail на клиенте включает fallback на keepalived. А в случае успешного
прохождения проверки выклкючает keepalived (подсовывает пустой конфиг), чтобы исключить races.
Для мастера monit-action.sh ничего не делает, предполагается что загорится мониторинг и надо
будет вручную разобраться что же случилось на ipvs-sync-server.

Juggler вызывает тот же самый скрипт monitoring.py.

Что проверяет monitoring.py:

- доступность rabbitmq: при выполнении ставится задача appstatus в брокер с FQDN сервера;
- проверяет время приема и ответа heartbeat сообщений и если оно не изменилось, то fail
- на стороне сервера проверяет время обновления данных воркеров  
(часто запускать не стоит, так как mapping обновляется не очень часто, см. конфигурацию)
- проверяет состояние очередей и если кол-во элементов в очереди больше 10, то ошибка

Общее представление мониторящихся величин:

    CHECKING_TIMINGS = {
        '/opt/venvs/ipvs-sync/bin/server.py': ['update_active_consumers', 'update_ipvs_tree',
                                               'update_services_mapping', 'update_vips_description'],
        '/opt/venvs/ipvs-sync/bin/client.py': ['send_heartbeat', '_func_heartbeat'],
    }
    CHECKING_QUEUES = {
        '/opt/venvs/ipvs-sync/bin/server.py': ['client_requests', 'processing'],
        '/opt/venvs/ipvs-sync/bin/client.py': ['announces']
    }


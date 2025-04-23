Сервис для обработки данных проходящих через LogBroker.
Например, можно фильтровать syslog-сообщения и отсылать в solomon количество совпадений.

Схема сервиса: \
[<img src="https://jing.yandex-team.ru/files/gescheit/syslog_snmptrapper%20%2812%29.jpg" width="1000"/>](https://jing.yandex-team.ru/files/gescheit/syslog_snmptrapper%20%2812%29.jpg)

Поддерживаются два типа входных данных. **mq** - данные из [grad](https://a.yandex-team.ru/arc/trunk/arcadia/noc/grad/docs)/[metridat-collector](https://a.yandex-team.ru/arc/trunk/arcadia/noc/metridat) и **[syslog](https://st.yandex-team.ru/NOCDEV-7205)**.

### Описание конфига

```yaml
HTTPPort: 12345
logging:
    level: info
pprof: true
invapi: # нужен для резолва src ip syslog в fqdn через RT
    oauth: "{{ invapi_token }}"
    url: "https://ro.racktables.yandex-team.ru/api"
logbroker_reader:
    database: "/Root"
    oauth_token: "{{ logbroker_token }}"
    consumer: "/grad/data/metridat_aggregator"
    topic:
        - "/grad/data/network"
        - "/noc/nocdev/syslog"

logbroker_writer: # запись результата агрегации метрик mq
    database: "/Root"
    oauth_token: "{{ logbroker_token }}"
    topic: "/grad/data/other"
    endpoint: "logbroker.yandex.net"

aggregators:
    network_magistral:
        type: mq
        topics:  # тут формат LB topic @ series name
            - "/grad/data/network@snmp_poller.network"
            - "/grad/data/network@snmp_poller.network_fast"
            - "/grad/data/network@comocutor_poller.network"
            - "/grad/data/network@comocutor_poller.network_fast"
            - "/grad/data/network@http_server.network"
        args:
            filter:
                keys:
                    ifalias: /.*(peer|client|transit)%.*/
            target: aggregator.external-links
    bfd_count:
        type: syslog
        topics:
            - "/noc/nocdev/syslog"
        args:
            message_filter: .*BFD session changed to Down.*
            sensor: bfd_down_count
```
Usage of aggregator:
```
-config string
  path to config file (default "config.yaml")
-dump
  dump output instead of real work
```

### Подготовка для запуска
Подготовка LogBroker:
```bash
export STAFF_LOGIN=<логин staff-пользователя, выполняющего инструкции>
export LOGBROKER_INSTALLATION=logbroker
export LOGBROKER_ENDPOINT=logbroker.yandex.net:2135

ya tool logbroker schema create directory /logbroker-playground/${STAFF_LOGIN} -y
ya tool logbroker schema create consumer /logbroker-playground/${STAFF_LOGIN}/metridat-aggregator-test-consumer -y --supported-codecs gzip,lzop,raw,zstd
ya tool logbroker permissions grant --subject ${STAFF_LOGIN}@staff --path /logbroker-playground/${STAFF_LOGIN}/metridat-aggregator-test-consumer --permissions ReadAsConsumer -y
ya tool logbroker schema create read-rule -t /noc/nocdev/syslog -c /logbroker-playground/${STAFF_LOGIN}/metridat-aggregator-test-consumer --all-original -y
```
[Получите токен для LogBroker](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=11515c5e5e994dfe8196ccfd6eb42dd8) и
[токен для Invapi](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=950f303bdd4446f3870c8d4156a1c1c9).

### Пример
Предположим, мы долго смотрели в syslog и заметили странное сообщение.
```
U 64:ff9b::8d08:9eec:64226 -> 2a02:6b8:0:3400:0:3c8:0:c:514 #175682
  <185>12747072: May 22 10:56:03: %HARDWARE-1-TCAM_ERROR: Found error in HQATM TCAM Space and not able to recover the error.-Traceback= 89DDF0 8A1270 8A1D94 703DC8 1535BF0 152C3C4
```
Теперь хотим сделать мониторинги по сообщению 'HARDWARE-1-TCAM_ERROR', для последующего алертинга. Делаем следующий конфиг:

```yaml
logging:
  level: "info"
invapi:
  oauth: "XXXX"
  url: "https://ro.racktables.yandex-team.ru/api"
logbroker_reader:
  database: "/Root"
  oauth_token: "XXXX" # указать полученный выше токен
  consumer: "/logbroker-playground/${STAFF_LOGIN}/metridat-aggregator-test-consumer" # STAFF_LOGIN заменить на свой
  topic:
    - &syslog "/noc/nocdev/syslog"
aggregators:
  tcam_error:
    type: "syslog"
    topics:
      - *syslog
    args:
      message_filter: "HARDWARE-1-TCAM_ERROR"
      sensor: "tcam_error"
      webhook: "http://localhost:12341/tcam_error"
```
Где message_filter это строка (поиск вхождения) или регулярка (обрамлена /).\
А sensor означает что данные надо отослать в solomon ([project=metridat, service=syslog_result](https://solomon.yandex-team.ru/?project=metridat&cluster=aggregator&service=syslog_result)) , а webhook - в указанную ручку.
Компилим ```ya make noc/metridat/internal/aggregator``` и запускаем с опцией -dump:
```bash
./noc/metridat/cmd/aggregator/aggregator -dump -config /path/to/config.yaml
```
В выводе могут быть логи самого демона (зависит от настроек level). Если всё хорошо, то видим наши совпадения:
```
2022-05-22T12:09:11.272+0300 INFO aggregator/aggregator.go:225 wait for rtAllocsApp update
...
syslog agg 'tcam_error' match host='iva2-i45.yndx.net' syslog='{"fromhost-ip":"64:ff9b::8d08:9eec","fromhost":"64:ff9b::8d08:9eec","timegenerated":"2022-05-29T19:28:43.042896+03:00","timestamp":"2022-05-29T19:28:42+03:00","host":"64:ff9b::8d08:9eec","severity":1,"facility":23,"syslog-tag":"%HARDWARE-1-TCAM_ERROR:","source":"%HARDWARE-1-TCAM_ERROR","msg":"Found error in HFTM TCAM Space and not able to recover the error#012-Traceback= 4D13A0 4D2590 703DAC 1535BF0 152C3C4"}'
increase sensors: increase tcam_error for host='iva2-i45.yndx.net'
send data to tcam_error http://localhost:12341/tcam_error {"data":{"fromhost-ip":"64:ff9b::8d08:9eec","fromhost":"64:ff9b::8d08:9eec","timegenerated":"2022-05-29T19:28:43.042896+03:00","timestamp":"2022-05-29T19:28:42+03:00","host":"64:ff9b::8d08:9eec","severity":1,"facility":23,"syslog-tag":"%HARDWARE-1-TCAM_ERROR:","source":"%HARDWARE-1-TCAM_ERROR","msg":"Found error in HFTM TCAM Space and not able to recover the error#012-Traceback= 4D13A0 4D2590 703DAC 1535BF0 152C3C4"},"uuid":"1edbc203-c2e8-45ea-a58e-5a62879ba979","hostname":"gescheit-osx"}
```
Тут "fromhost-ip":"64:ff9b::8d08:9eec" маппинг из [rfc6052](https://www.ietf.org/rfc/rfc6052.txt), завернутый в [udp-balaner](https://a.yandex-team.ru/arc/trunk/arcadia/noc/udp-balancer/rawip.go?rev=r9455120#L43). \
После выкатки правок в прод, в соломоне будет такой график: \
[<img src="https://jing.yandex-team.ru/files/gescheit/Screenshot%202022-05-29%20at%2021.03.50.png" width="1000"/>](https://jing.yandex-team.ru/files/gescheit/Screenshot%202022-05-29%20at%2021.03.50.png)
А в webhook будут прилетать запросы вида:
```shell
{'data': {'facility': 23,
          'fromhost': '64:ff9b::8d08:9eec',
          'fromhost-ip': '64:ff9b::8d08:9eec',
          'host': '64:ff9b::8d08:9eec',
          'msg': 'Found error in HFTM TCAM Space and not able to recover the '
                 'error#012-Traceback= 4D13A0 4D2590 703DAC 1535BF0 152C3C4',
          'severity': 1,
          'source': '%HARDWARE-1-TCAM_ERROR',
          'syslog-tag': '%HARDWARE-1-TCAM_ERROR:',
          'timegenerated': '2022-05-29T19:18:09.943675+03:00',
          'timestamp': '2022-05-29T19:18:08+03:00'},
 'hostname': 'ololo-osx',
 'uuid': 'd3e2b3c9-c023-4dbe-83e6-51c1d5b01554'}
```
Поля в data определяются в rsyslog ([структура](https://a.yandex-team.ru/arc/trunk/arcadia/noc/metridat/internal/aggregator/syslog.go?rev=r9516477#L38)).\
Если не прилетают заросы, то надо проверить [наличие дырок](https://puncher.yandex-team.ru/?rules=exclude_inactive&sort=source&source=_C_NOCDEV_METRIDAT_AGGREGATOR_).

### Разработка
Если были изменения структур под //easyjson:json, то вызываем go generate:
```shell
ya make . ---add-protobuf-result
ya tool go generate -v -x ./...
```

### Отладка Unified Agent
Повторить pull-запрос соломон можно так:
```shell
curl -H 'X-Solomon-FetcherId: 1' 'http://localhost:11003/read?project=metridat&service=syslog_result'
```
где ```read?project=metridat&service=syslog_result``` запрос из настроек шарда в solomon.

А так можно сделать запрос в сам metridat-aggregator:
```shell
curl -s 'http://localhost:12345/metrics/syslog_result' | jq .                                                                                                                                                                  13:11

{
  "metrics": [
    {
      "type": "COUNTER",
      "labels": {
...
```
Выкатка конфигов:
```shell
executer p_exec %nocdev-metridat-aggregator "salt-call state.highstate queue=true"
```

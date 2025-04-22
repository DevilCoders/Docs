# B2Bgeo Egts Proxy

[[toc]]

## General information
| What | Where |
| ---- | --- |
| Сервис в ABC | [maps-b2bgeo-egtsproxy](https://abc.yandex-team.ru/services/maps-b2bgeo-egtsproxy/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_B2BGEO_EGTSPROXY |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stress | [maps_b2bgeo_egtsproxy_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_egtsproxy_stress/) | [ b2bgeo-egtsproxy.stress ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-egtsproxy-stress-panel-main/) | [ maps_b2bgeo_egtsproxy_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_egtsproxy_stress) |
| Testing | [maps_b2bgeo_egtsproxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_egtsproxy_testing/) | [ b2bgeo-egtsproxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-egtsproxy-testing-panel-main/) | [ maps_b2bgeo_egtsproxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_egtsproxy_testing) |
| Prestable | [maps_b2bgeo_egtsproxy_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_egtsproxy_prestable/) | [ b2bgeo-egtsproxy.prestable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-egtsproxy-prestable-panel-main/) | [ maps_b2bgeo_egtsproxy_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_egtsproxy_prestable) |
| Stable | [maps_b2bgeo_egtsproxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_egtsproxy_stable/) | [ b2bgeo-egtsproxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-egtsproxy-stable-panel-main/) | [ maps_b2bgeo_egtsproxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_egtsproxy_stable) |


[Monitorings all (tag=a_prj_maps-b2bgeo-egtsproxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-b2bgeo-egtsproxy)


### L3 Balancer

| Staging | L3 Balancer |
| ------- | ----------- |
| Testing | https://l3.tt.yandex-team.ru/service/11715 |
| Prestable, stable | https://l3.tt.yandex-team.ru/service/12047 |

### Firewall macroses

| Staging | URL |
|---|---|
| Testing, stress | [ \_MAPS_B2BGEO_EGTSPROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_EGTSPROXY_TESTING_RTC_NETS_ ) |
| Prestable, stable | [ \_MAPS_B2BGEO_EGTSPROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_EGTSPROXY_STABLE_RTC_NETS_ ) |


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/* |

### Raw data log
| Name | URL/path |
|---|---|
| Locally | /logs/raw_data.log |
| YT testing | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/b2bgeo-egts-test-raw-log |
| YT stable, prestable | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/b2bgeo-egts-raw-log |

### Yacare service log
| Name | URL/path |
|---|---|
| Locally | /var/log/yandex/maps/egts-proxy/* |
| YT testing | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/b2bgeo-egts-proxy-testing |
| YT stable, prestable | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/b2bgeo-egts-proxy-stable |


## Technical info
Есть компании, которые ходят по IP. Обнаружить таких клиентов невозможно, потому что в заголовках tcp/ip пакетов нет данных о hostname.


## Running modes

### Server mode

When started as server (`--server --port <port>`), binds to provided TCP port on all ipv4 interfaces (0.0.0.0).
Logs are written to stdout as newline-separated json.
Env variables `YA_COURIER_BACKEND_OAUTH_KEY` and `YA_COURIER_BACKEND_URL` must be defined to send messages to ya-courier-backend.

```(bash)
# listen for TCP 4000
./egts-proxy --server --port 4000

# validate (should print long parsed packet as text, and produce log messages)
cat testdata-positions/2072370.bin | nc 127.0.0.1 4000 | ./egts-proxy --dump-req-text --input -
```

### Server in dump mode

It is possible to dump individual EGTS packets received from defined terminal, as well as responses sent by server. When egts-proxy is deployed, it is possible to restart service locally with custom env variable to enable dumping behavior:

```(bash)
# ssh to <backend hostname>
$ cd app
$ kill -9 `pidof egts-proxy` && DEBUG_DUMP_TID=1234 ./egts-proxy --server --port 4000
```

In the example above, service is killed, and port 4000 is acquired on start, leaving supervisor without a chance to restart the service.

When new EGTS message for terminal with TID=1234 will be received, it is saved under current directory as `1234.req.1.bin` for first received packet, `1234.req.2.bin` for second, and so on. Responses are saved under same directory, for each received packet (`1234.1.rep.bin` for example above).

### Inspector mode

Inspector mode is useful for debugging and inspection of request and response in EGTS format.

```(bash)
# dump binary input in EGTS format as text to stdout
./egts-proxy --dump-req-text --input <path or "-" for stdin>

# dump EGTS response in binary format, generated after parsing EGTS input
./egts-proxy --dump-rep-binary --input <path or "-" for stdin>

# dump EGTS response in text format
./egts-proxy --dump-rep-binary --input <path or "-" for stdin> | ./egts-proxy --dump-req-text --input -
```

## Environment variables
Some of the following variables are taken from YaVault secrets and are specified in sedem config ([link](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/egts-proxy/sedem_config/secrets.yaml)).

|  Variable |  Description |  Example |
|---|---|---|
| YA_COURIER_BACKEND_URL | URL of Ya Courier Backend | https://courier.yandex.ru |
| YA_COURIER_BACKEND_OAUTH_KEY | robot-egts OAuth token | something |
| PG_HOST | Postgres DB host | man-y2gsze837xkti49s.db.yandex.net,sas-f8qxanthr6o0js89.db.yandex.net,vla-8as5ajxlrauvbuxd.db.yandex.net |
| PG_PORT | Postgres DB port | 6432 |
| PG_ARGS | Postgres DB extra args: dbname, user, password | dbname=b2bgeo_egts_prod user=dbuser password=xxx |
| YCR_SKIP_CONF | Yacare skips checking of the config, see BBGEO-6639 | defined |
| TVM_SECRET | Service tvm secret | something |
| LOGS_DIR | Raw log dir | / |
| EGTS_PG_CONNECTION_COUNT | Number of connections to Postgres | 30 |
| EGTS_IO_SERVICE_THREADS | Number of threads for incoming requests | 10 |
| EGTS_HTTP_SUBMITTER_THREADS | Number of threads for outgoing requests to Ya Courier Backend | 10 |


## Deploy process
1. After each commit testenv builds docker image (link [here](#general-information])).
When it's ready you will receive email from sandbox.
2. When docker image is ready check it with `ya tool sedem release info maps/b2bgeo/ya_courier/egts-proxy`.
3. Now you can deploy any revision from `Release candidates` to testing with `ya tool sedem release start maps/b2bgeo/ya_courier/egts-proxy rXXXXXXX`.
4. If everything is ok deploy version from testing to prestable: `ya tool sedem release step maps/b2bgeo/ya_courier/egts-proxy vX.X prestable`.
5. Wait for 24 hours. Deploy to stable: `ya tool sedem release step maps/b2bgeo/ya_courier/egts-proxy vX.X stable`.
5. You are perfect!


## Troubleshooting

https://wiki.yandex-team.ru/b2bgeo/dev/helpdesk/troubleshooting/#egts-proxy


## Wiki page

https://wiki.yandex-team.ru/b2bgeo/dev/yacourier/egts-proxy/


## Tools

### Replay tool
Prerequisites: YT token is stored in `~/.yt/token` or environment variable `YT_AUTH_TOKEN` is specified.

Arguments:
* `--table` - YT table with dumped data from EGTS-proxy server in production. Path: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/b2bgeo-egts-raw-log
* `--host` - server host to send replaying data
* `--port` - server port to send replaying data

Important: you should increase number of open files in ulimit up to number of session in table to be replayed, e.g.: `ulimit -n 30000`.

Example:
```
$arcadia/maps/b2bgeo/ya_courier/egts-proxy/tools/replay ./replay --port 4000 --table //home/logfeller/logs/b2bgeo-egts-raw-log/30min/2020-12-27T18:00:00 --host b2bgeo-egts-proxy.testing.maps.yandex.net -v
```

### Stress load tool
[Readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/egts-proxy/tools/stress_load/README.md)

### Health check tool
[Readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/egts-proxy/tools/health_check/README.md)


### Расшифровать пакет
В `/arcadia/maps/b2bgeo/ya_courier/egts-proxy/tools/parser` лежит парсер, которому можно дать на вход hex-представление пакета и получить его расшифровку по полям.

```
$~/arcadia/maps/b2bgeo/ya_courier/egts-proxy/tools/parser ya make -r
$~/arcadia/maps/b2bgeo/ya_courier/egts-proxy/tools/parser ./parser --hex $package_hex_dump
```


## Crash course по протоколу EGTS

### Транспортный уровень
На транспортном уровне (TransportPacketHeader) информации про терминал, oid, tid и imei нет
В пакете есть поле SFRD = Services Frame Data - протокол уровня поддержки услуг
PT - тип транспортного пакета
  0 - EGTS_PT_RESPONSE (подтверждение на пакет транспортного уровня);
  1 - EGTS_PT_APPDATA (пакет, содержащий данные протокола уровня поддержки услуг);
  2 - EGTS_PT_SIGNED_APPDATA (пакет, содержащий данные протокола уровня поддержки услуг с цифровой подписью).

Пример выдачи нашего парсера пакета (PT=1, пакет с данными уровня поддержки услуг):
```cpp
  TransportPacketHeader:
    PRV:  1     // protocol version, always 0x01;
    SKID: 0     // security key id;
    PRF:  0
    HL:   11    // header length in bytes including the check sum byte (HCS field);
    HE:   0     // header encoding;
    FDL:  15    // SFRD field length;
    PID:  1     // Transport Level package number
    PT:   1     // packet type, EGTS_PT_RESPONSE = 0, EGTS_PT_APPDATA = 1, EGTS_PT_SIGNED_APPDATA = 2
    HCS:  6     // CRC8 checksum of packet
```

Формат SFRD Для EGTS_PT_APPDATA:
  - SDR1, SDR2, SDR3

### Уровень поддержки услуг
Формат отдельной записи протокола уровня поддержки услуг (Service Record Header)

Пример
```cpp
 ServiceRecordHeader:
      RL*:  8   // length of RD field in bytes
      RN*:  1   // record number (packet counter)
      RFL*: 0   // record flags, see specification
      OID:  0   // optional, source or target unique object identifier (normally IMEI)
      EVID: 0   // optional, unique event identifier
      TM:   0   // optional, record creation time (sec since EGTS_TIMESTAMP_START)
      SST*: 1   // source EGTS service type (=EGTS_TELEDATA_SERVICE)
      RST*: 1   // recepient EGTS service type (=EGTS_TELEDATA_SERVICE)
```
  - Record Flags - RFL (Record Flags) содержит битовые флаги, определяющие наличие в данном пакете полей OID, EVID и ТМ, характеризующих содержащиеся в записи данные;
  - OID (Object Identifier) - идентификатор объекта, сгенерировавшего данную запись или для которого данная запись предназначена (уникальный идентификатор АСН), либо идентификатор группы (при GRP=1). При передаче от АСН в одном пакете транспортного уровня нескольких записей подряд для разных сервисов, но от одного и того же объекта, поле OID может присутствовать только в первой записи, а в последующих записях может быть опущено;
  - SST  (source service type)
  - RST (recipient service type)

//Типы в SST / RST//
  -  EGTS_AUTH_SERVICE = 1,   // This service is intended for ST authentication at TP. When using the TCP/IP protocol ST should pass this procedure,
                                // and further interaction is possible only if the procedure
                                // is completed successfully.
  - EGTS_TELEDATA_SERVICE = 2,  // Передача данных (координат, сенсоров и т.п.)
  - EGTS_COMMANDS_SERVICE = 4,  // Мы не поддерживаем
  - EGTS_FIRMWARE_SERVICE = 9,  // Мы не поддерживаем
  - EGTS_ECALL_SERVICE = 10     // Мы не поддерживаем

После заголовка идёт поле RD = Record Data. Содержит информацию, присущую определенному типу сервиса (одну или несколько подзаписей сервиса типа, указанного в поле SST или RST, в зависимости от вида передаваемой информации).

### Подзаписи Record Data
Сначала идёт заголовок из двух записей (тип, длина), после этого данные (SRD).
  - SRT  (type)
  - SRL (length)
  - SRD (subrecord data)

#### Подзаписи EGTS_AUTH_SERVICE
В Service Record Header был передан SST=EGTS_AUTH_SERVICE=1
- SRT = EGTS_SR_TERM_IDENTITY = 1
В нём содержится
- TID (Terminal Identifier) - уникальный идентификатор, назначаемый при программировании АСН. Наличие значения 0 в данном поле означает, что АСН не прошла процедуру конфигурирования или прошла ее не полностью. Данный идентификатор назначается оператором и однозначно определяет набор учетных данных АСН. TID назначается при инсталляции АСН как дополнительного оборудования и передаче оператору учетных данных АСН (IMSI, IMEI, serial_id). В случае использования АСН в качестве штатного устройства, TID сообщается оператору автопроизводителем вместе с учетными данными (VIN, IMSI, IMEI);
В этом же пакете может приходить IMEI (но он опционален)
- FLG (флаги, означающие наличие полей HDID, IMEI, IMSI, LNGC и т.п. Наша реализация их не поддерживает.

#### Подзаписи с EGTS_TELEDATA_SERVICE
В Service Record Header был передан SST=EGTS_TELEDATA_SERVICE=2
Идентификация: для записи teledata service есть только oid. Если мы не находим соответствующий tid, то присвоим записи tid = oid

Поддерживаемые нами SRT (отправка координат):
- EGTS_SR_POS_DATA = 16,
- EGTS_SR_EXT_POS_DATA = 17,

[Заголовочный файл с реализацией](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/egts-proxy/egts/protocol.hpp?rev=7437578#L116)

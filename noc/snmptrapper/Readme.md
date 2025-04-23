Сервис для приема SNMP trap, форматирование их в удобный вид и запись в Unified Agent для последующего хранения в YT.
Так-же поддерживается вызов web-hook.

[<img src="https://jing.yandex-team.ru/files/gescheit/syslog_snmptrapper%20%289%29.jpg" width="1000"/>](https://jing.yandex-team.ru/files/gescheit/syslog_snmptrapper%20%289%29.jpg)

### Конфигурация
Сервис лежит в пакете snmptrapper. Установить можно командой:
```shell
apt-get install snmptrapper
```

Формат конфигурации:
```yaml
map: # Соотношение между oid и именем
  "1.3.6.1.2.1.1.3.0": { "name": "uptime" }
  "1.3.6.1.4.1.13238": { "name": "yandex" }
syslog_RPS: 1000 # Максимальный RPS посылки в syslog
syslog_host: "127.0.0.1:514"  # Syslog назначение
grpc_host: "127.0.0.1:12345"  # UA GRPC хоста
output_format: "syslog"  # тип выходных данных syslog/JSON
listen_udp_host: 162  # Порт для приема UDP
metrics: # конфиг метрик из a.yandex-team.ru/noc/go/metrics. По умолчанию включен pull
web_hooks:  # подписка на веб-хуки
  cfglister:  # id
    oid_names:
      - linuxCommitAPI
      - hwCfgChgNotify # huawei
    receiver: "http://host:22111/trap/"
    post_fn: config
```

Дублирование в разные приемники не поддерживается, поэтому следует указывать один из параметров **syslog_host**/**grpc_host**.
Конфиги разбиты на две части. Конфигурация трансляции OID в имя в [snmptrapper](https://a.yandex-team.ru/arc/trunk/arcadia/noc/snmptrapper/configs/) и выкатывается вместе с пакетом.
Конфигурация с паролем и прочим лежит в [salt](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-snmptrap/files/etc/snmptrapper/config.yml) и выкатывается отдельно руками.

### Веб-хуки
В конфигурации в поле web_hooks указывается на какие данные нужно дергать веб-хуки. Поддерживается только фильтрация по trap oid. Сервис дергает вуб-хуки с
экспоненциальным таймаутом до 15 минут. Ожидается ответ 2xx. Запросы делаются с адреса макросов [\_C_NOCDEV_SNMPTRAP\_](https://puncher.yandex-team.ru/?create_protocol=tcp&create_sources=_C_NOCDEV_SNMPTRAP_&create_until=persistent).\
Пример приемника данных:
```python
from aiohttp import web

async def handle(request):
    body = await request.json()
    print(body)
    return web.Response(text="OK")

app = web.Application()
app.add_routes([web.post('/trap/', handle)])

if __name__ == '__main__':
    web.run_app(app, port=22111)
```
В теле запроса в поле data сам SNMP trap данные:
```
{'recv_timestamp': 1652176174,
 'receiver': 'vla-snmptrap1.net.yandex.net',
 'sender_fqdn': 'vla2-9s38.yndx.net',
 'sender_ip': '172.24.213.133',
 'uuid': 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
 'format': 'format',
 'data': {'hwCfgBaselineTime.0': '2021-01-25 14:35:54',
          'hwCfgChgSeqIDReveralCount.0': '0',
          'hwCfgChgTableMaxItem.0': '10000',
          'hwCurrentCfgChgSeqID.0': '886',
          'snmpTrapOID': 'hwCfgChgNotify',
          'uptime': '193605931'}
 }
```
Структура доступна для импорта в [snmptrapper/pkg/snmptrap](https://a.yandex-team.ru/arc/trunk/arcadia/noc/snmptrapper/pkg/snmptrap/snmptrap.go).

#### post_fn

Существует возможность обработать трапы перед отправкой. Например, для того чтобы избавится от вендорской специфики.
В таком случае в data будут данные в другом формате, а в format будет указано что-то вроде названия postfn.
Эти значения определяются реализацией интерфейса WebHookPayload (смотри [пример](https://a.yandex-team.ru/svn/trunk/arcadia/noc/snmptrapper/pkg/snmptrap/postfn.go?rev=r9594341#L36)).

### YT
Все получаемые данные отправляются в Unified-Agent через GRPC. Через LogBroker и LogFeller данные в итоге попадают в YT.
Учтите, что в YT данные приезжают каждый 30 минут, а не в реальном времени.

Формат парсинга [LogFeller](https://a.yandex-team.ru/arc_vcs/logfeller/configs/parsers/nocdev-snmptrap-log.json). \
Данные в [YT](https://yt.yandex-team.ru/hahn/navigation?path=//logs/nocdev-snmptrap-log/30min/).
[Графики записи в LB](https://logbroker.yandex-team.ru/logbroker/accounts/noc/nocdev/snmptrap?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1652362769225&metricsTo=1652366369225&sortOrder=%22default%22)
и [Графики поставки logfeller](https://solomon.yandex-team.ru/?project=logfeller&cluster=hahn&service=indexing&dashboard=logfeller-log-life-index&autorefresh=y&l.stream-name=noc%40nocdev-snmptrap).

#### Примеры запросов
[Трапы за текущий день](https://yql.yandex-team.ru/Queries/628cd39897c5b72aadb90cc8) от хоста sofino-u12.yndx.net и трап = hwPoePowerOn:
```sql
USE hahn;
$today  = DateTime::Format("%Y-%m-%d")(CurrentUtcDateTime());

SELECT `host`, `msg`, `timestamp`
FROM RANGE(`//logs/nocdev-snmptrap-log/30min`, $today)
WHERE Yson::ConvertToString(Yson::YPath(msg, "/snmpTrapOID"))  = 'hwPoePowerOn'
AND host= 'sofino-u12.yndx.net'
ORDER BY timestamp
```

Пример результата: \
[<img src="https://jing.yandex-team.ru/files/gescheit/Screenshot%202022-05-24%20at%2016.28.40.png" width="900"/>](https://jing.yandex-team.ru/files/gescheit/Screenshot%202022-05-24%20at%2016.28.40.png)

Из-за особенностей хранения данных, [запрос за последние 7](https://yql.yandex-team.ru/Queries/6282c805d2706c24f8430ebe) дней выглядит посложнее:
```sql
USE hahn;
$base_path = "logs/nocdev-snmptrap-log";
$num_days = 7;

$today = CurrentUtcDate();
$window = CAST("P" || CAST($num_days AS string) || "D" AS Interval);
$first_day = $today - $window;

$table_paths_1d = (SELECT AGGREGATE_LIST(Path) FROM (
    SELECT Path
    FROM FOLDER($base_path || "/1d")
    WHERE Type = "table"
    AND CAST(TableName(Path) AS date) BETWEEN $first_day AND $today
));

$tables_paths_30min = (SELECT AGGREGATE_LIST(Path) FROM (
    SELECT Path
    FROM FOLDER($base_path || "/30min")
    WHERE Type = "table"
));

SELECT `host`, `msg`, `timestamp`
FROM EACH(ListExtend($table_paths_1d, $tables_paths_30min))
WHERE Yson::ConvertToString(Yson::YPath(msg, "/snmpTrapOID"))  = 'hwPoePowerOn'
ORDER BY timestamp
```

### Архитектура

[<img src="https://jing.yandex-team.ru/files/gescheit/syslog_snmptrapper%20%288%29.jpg" width="800"/>](syslog_snmptrapper.jpg)

Пароль от робота robot-snmptrap https://yav.yandex-team.ru/secret/sec-01g2a36gvs83sm0jtnar8j446g/explore/version \
Секреты используемые в самом snmptrapper https://yav.yandex-team.ru/secret/sec-01g2a4gz27ehy921g7cfhftc6c/explore/version \
Кондукторная группа https://c.yandex-team.ru/groups/nocdev-snmptrap
### Мониторинги
Кулебяки [тут](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/kulebyaks/nocdev/nocdev-snmptrap.yaml). \
Juggler [dashboard](https://juggler.yandex-team.ru/dashboards/snmptrap/). \
<iframe height="400" width="100%" frameborder="0" src="https://monitoring.yandex-team.ru/embed/snmptrapper/dash/monidfmin34sek8t094o?from=now-1d&to=now"></iframe>

Дашборд https://monitoring.yandex-team.ru/projects/snmptrapper/dashboards/monidfmin34sek8t094o?from=now-1d&to=now&refresh=60000 \
[Статус сервиса](https://slb.yandex-team.ru/service?service=noc-snmptrap.yandex.net) в slb
### Разработка
#### Деплой
Пакет автоматом собирается в CI и выкладывается в dist noc/testing. Чтобы выложить в прод, в CI запускаем действие "Deploy snmptrapper".
Конфиги катить руками через salt ```salt-call state.highstate queue=true``` в кондукторной группе [nocdev-snmptrap](https://c.yandex-team.ru/groups/nocdev-snmptrap).

#### SNMP trap формат

[<img src="https://jing.yandex-team.ru/files/gescheit/snmptrap.png" width="600"/>](snmptrap.png)

SNMP-trap представляет собой SNMP-пакет у которого в varbind list части передаются данные о трапе.
varbind list представляется из себя список, каждый элемент которого это ключ и значение.
Формат ключа всегда object ID (например 1.3.6.1.2.1.1.3.0), а value может быть разных типов (вроде строки или числа)
декодируется в словарь у которого обязательно есть поле snmpTrapOID.

В SNMP v2 имя трапа передается в varbind list с ключом 1.3.6.1.6.3.1.1.4.1.0 и представляет object ID.
В случае [SNMP trap v1](https://nda.ya.ru/t/_Mt9X-c057bCw9), используются дополнительные специальное поля для имени трапа и времени.

Для резолва OID в что-то более читабельное в конфигурации указан маппинг OID -> name. OID из значения тоже резолвится.
```yaml
map:
    "1.3.6.1.4.1.2011.5.25.207.1.5.5": { "name": "hwCurrentVty" }
    "1.3.6.1.4.1.2011.5.25.207.1.5.6": { "name": "hwMaxVty" }
```

Если необходимо добавить новый OID, то есть несколько способов найти имя.
1. Установить куда-нибудь в свою систему все возможные MIB файлы и использовать snmptranslate.
2. Поискать в интернете. Например, [oidref](https://nda.ya.ru/t/Ljc8xOn857bDAx), [snmptrans](https://nda.ya.ru/t/r4GZQNpW57bDJa) или просто в поиске.
3. В редких случаях интернет может ничего не знать про трапы, например что-то совсем новое. В таких случаях нужно смотреть документацию вендоров.
Например, huawei иногда в xls-файлах с изменениями указывает новые трапы.
У juniper есть [поиск по своим MIB](https://nda.ya.ru/t/6ayFOc2a57bCyE) и [общий поиск у huawei](https://nda.ya.ru/t/x95aWVIU57bCz6).

Нужно учесть что часть OID может быть индексом. 1.3.6.1.4.1.2011.5.25.38.2.3.1.21.**18573** - тут индекс 18573,
но может состоять из нескольких чисел. Автоматика работает как LPM и выдает наиболее точную ассоциацию конкатенируя
к ней индексную часть.
Для резолва индекса в более читаемой вид, нужно указать в конфигурации:
```yaml
map:
    "1.3.6.1.4.1.30065.4.1.1.3.1.1": { "name": "aristaBgp4V2PeerLastErrorCodeReceived",
                                       "index": [ "Unsigned32 (1..4294967295)",
                                                  "INTEGER {unknown(0), ipv4(1), ipv6(2), ipv4z(3), ipv6z(4), dns(16)}",
                                                  "OCTET STRING (0..255)" ]
```
Такая настройка декодирует так:
```
1.3.6.1.4.1.30065.4.1.1.3.1.1.1.2.16.1.1.0.0.11.42.0.0.0.0.0.0.0.4.0.1
1.3.6.1.4.1.30065.4.1.1.3.1.1 -> aristaBgp4V2PeerLastErrorCodeReceived
1 -> 1
2 -> ipv6
16 -> Размер IP, пропускаем.
1.1.0.0.11.42.0.0.0.0.0.0.0.4.0.1 - > 1:1:0:0:0B:2A::04:0:1
```
У значения есть тип ([rfc2578](https://nda.ya.ru/t/Adu_kaIP57bC8K)), но этого не всегда достаточно для корректного представления.
Например, MAC-адрес передается как набор байтов, и чтобы декодировать его в строковое представление, нужно указать syntax:
```yaml
map:
    "1.3.6.1.4.1.9.9.215.1.3.3": { "name": "cmnMACMoveAddress",
                                   "syntax": "MacAddress" }
```

В cmd/mib_parser есть утилита для парсинга MIB-file. Пример запуска: ```mib_parser.py -d HUAWEI-L2MAM-MIB```.
В итоге получается что-то похожее на map, но требуется дальнейшая разработка для нормально парсинга MIB-файлов.

#### Типичные проблемы
Упячка в данных:
```shell
"jnxDomCurrentLaneAlarmDate.852\":\"\\u0007\\ufffd\\u0005\\u0018\\u00122%\\u0000+\\u0003\\u0000\"
```
Это представление байтов в виде юникодной строки. Проблема возникает из-за того, что в самом пакете есть только тип данных и иногда этого недостаточно для корректного отображения.
В данном случае формат данных octet string - просто набор байтов. Если бы там были ASCII, то текст был бы корректно отображен, но тут просто набор байтов.
Чтобы понять как его представить, нужно искать доку и указать syntax для этого OID. В этом примере нужно добавить ```"syntax": "DateAndTime"```.
Список поддерживаемых типов смотри в [internal/snmp/syntax_parser.go](https://a.yandex-team.ru/arc/trunk/arcadia/noc/snmptrapper/internal/snmp/syntax_parser.go?rev=r9497843#L21).

#### Собираем диагностику
```
tcpdump -i any -w /tmp/pcap.pcap port 162
```
После чего можно поискать нужные пакеты по фильтру:
```
tshark -r /tmp/pcap.pcap -t ad "snmp.name contains 1.3.6.1.4.1.2011.5.25.315.3.5"
```

### Тестирование
Запуск сервиса в режиме вывода сообщения, вместо отсылки:
```shell
snmptrapper -f -d -c config.yaml
```

Послать тестовый трап:
```shell
snmptrap -v 2c -c public localhost '' 1.3.6.1.4.1.13238.2 1.3.6.1.4.1.13238.2.1 s root 1.3.6.1.4.1.13238.2.2 i 2
```

tail сообщений в из UA:

```shell
unified_agent select --storage syslog_storage -f
```

В зависимости от настроек, в journald могут логгироваться не только ошибки, но и все отладочные данные.
```shell
journalctl -u snmptrapper.service -n 10
-- Logs begin at Fri 2022-05-20 11:37:24 MSK, end at Tue 2022-05-24 15:22:51 MSK. --
мая 24 15:22:51 sas-snmptrap1.net.yandex.net snmptrapper[70768]: 2022-05-24T15:22:51.106+0300        DEBUG        internal/ua_grpc.go:42        send        {"msg": "{\"timestamp\":1653394971,\"host\":\"sas1-s153.yndx.net\",\"snmp_trap_OID\":\"hwXQoSNotifications.51\",\"msg\":{\"uptime\":\"100503397\",\"snmpTrapOID\":\"hwXQoSNotifications.51\",\"hwXQoSPacketsDropInterfaceAlarmIfName.7.71.69.49.47.48.47.56.2.1.49\":\"GE1/0/8\",\"hwXQoSPacketsDropInterfaceAlarmQueueId.7.71.69.49.47.48.47.56.2.1.49\":\"2\",\"hwXQoSPacketsDropInterfaceAlarmSlotId.7.71.69.49.47.48.47.56.2.1.49\":\"1\"}}"}
мая 24 15:22:51 sas-snmptrap1.net.yandex.net snmptrapper[70768]: 2022-05-24T15:22:51.148+0300        DEBUG        internal/ua_grpc.go:42        send        {"msg": "{\"timestamp\":1653394971,\"host\":\"sas1-s254.yndx.net\",\"snmp_trap_OID\":\"hwXQoSNotifications.51\",\"msg\":{\"uptime\":\"100526330\",\"snmpTrapOID\":\"hwXQoSNotifications.51\",\"hwXQoSPacketsDropInterfaceAlarmIfName.7.71.69.49.47.48.47.55.2.1.49\":\"GE1/0/7\",\"hwXQoSPacketsDropInterfaceAlarmQueueId.7.71.69.49.47.48.47.55.2.1.49\":\"2\",\"hwXQoSPacketsDropInterfaceAlarmSlotId.7.71.69.49.47.48.47.55.2.1.49\":\"1\"}}"}
мая 24 15:22:51 sas-snmptrap1.net.yandex.net snmptrapper[70768]: 2022-05-24T15:22:51.316+0300        DEBUG        internal/ua_grpc.go:42        send        {"msg": "{\"timestamp\":1653394971,\"host\":\"vla1-1s169.yndx.net\",\"snmp_trap_OID\":\"hwLocalFaultAlarmResume\",\"msg\":{\"hwPhysicalPortName.31\":\"10GE1/0/27\",\"uptime\":\"108804334\",\"snmpTrapOID\":\"hwLocalFaultAlarmResume\",\"hwPhysicalPortIfIndex.31\":\"31\"}}"}
```

Если были изменения структур под ```//easyjson:json```, то вызываем go generate:
```shell
ya tool go generate -v -x ./...
```

### Статьи
[https://www.syslog-ng.com/technical-documents/doc/syslog-ng-open-source-edition/3.16/administration-guide/8](https://nda.ya.ru/t/VfcIWbhJ57bDmz) \
[https://techblog.bozho.net/the-syslog-hell/](https://nda.ya.ru/t/FZCFs-k957bDeP) \
[https://mibs.observium.org/mib/HUAWEI-XQoS-MIB/](https://nda.ya.ru/t/Dy1ahqOR57bDci) - для резолва OID. \
[https://net-snmp.sourceforge.io/wiki/index.php/TUT:snmptrap](https://nda.ya.ru/t/2J4vqVpN57bDbd) - про SNMP trap \
[https://www.webnms.com/snmp/help/snmpapi/snmpv3/table_handling/snmptables_basics.html](https://nda.ya.ru/t/bxRsUI1y57bDbJ) - про SMI

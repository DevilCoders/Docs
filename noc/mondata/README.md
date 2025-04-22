Сервис mondata отвечает за создание алертов в solomon/juggler/zabbix а так же за доставку конфигов и проверок для zabbix-agent и juggler-client.

Части сервиса:
- juggler-агрегаты (устаревшая). Автоматика для синхронизации агрегатов. [Подробности](https://a.yandex-team.ru/arcadia/noc/mondata/juggler/README.md "readme")
[агрегаты](https://a.yandex-team.ru/arcadia/noc/mondata/juggler/README.md "readme")
- juggler-оповещения (устаревшая). Автоматика для синхронизации оповещений. [Подробности](https://a.yandex-team.ru/arcadia/noc/mondata/juggler/README.md "readme")
[агрегаты](https://a.yandex-team.ru/arcadia/noc/mondata/juggler_notify/README.md "readme").
- solomon-алерты (устаревшая). Автоматика для синхронизации алертов в solomon. [Подробности](https://a.yandex-team.ru/arcadia/noc/mondata/juggler/README.md "readme")
[агрегаты](https://a.yandex-team.ru/arcadia/noc/mondata/solomon/README.md "readme")
- Кулебяки. Автоматика для синхронизации solomon-алертов, juggler-агрегатов и juggler-оповещений. [Подробности](https://a.yandex-team.ru/arcadia/noc/mondata/kulebyaks/README.md "readme")

В [/noc/mondata](https://a.yandex-team.ru/arc/trunk/arcadia/noc/mondata) лежат генераторы проверок, а скрипты для
синхронизации их лежат в [/noc/packages/mondata_server](https://a.yandex-team.ru/svn/trunk/arcadia/noc/packages/mondata_server)

### Zabbix-discovery

### Развертывание окружения для разработки
Чтобы корректно склонировать все части проекта выполняем:
python3 -m pip install --user -U -r requirements.txt

В папке **discovery** лежат скрипты, генеряшие список проверок.
Сами проверки лежат в **check**. Генератор проверок можно проверить запустив скрипт.

### Добавление проверки
#### 1. Создать скрипт проверки. Опционально
В папке **check** лежат скрипты, которые могут быть запушены на целевом сервере или на сервере мониторинга.
Если нет подходящего скрипта, то нужно создать свой. Скрипт должен возвращать OK, если все хорошо. Либо текст ошибки.
Так как папка check разъезжается по серверам по не очень безопасным каналам, то не следуют там хранить чувствительную информацию.
Для скриптов на питоне, использующих внешние модули, существует папка virtualenv в которой лежат модули.
Эта папка разъезжается по серверам вместе с проверками и подключается так: ```export PYTHONUSERBASE=virtualenv/arch```.

#### 2. Создать скрипт генерации проверки
В папке **discovery** лежат скрипты, которые генерируют JSON, в котором написано на каких хостах и что нужно проверять.
Пример скрипта:
```python
# AUTHOR: user@yandex-team.ru
import json

from helpers import check_script_status, get_rt_hosts

def make_checks():
    fqdns = get_rt_hosts('{сервер АСУ} and {Ubuntu}')
    check = check_script_status(hosts=fqdns,
                                script_name="resolver.sh",
                                service="dns",
                                description="{ITEM.LASTVALUE1}",
                                priority="INFO",
                                tags=["DNS"],
                                help_key="resolverproblem"
                                )
    return check

if __name__ == '__main__':
    print(json.dumps(make_checks(), indent=2))

```
AUTHOR нужно всегда указывать, чтобы получать оповещения о проблемах при выполнении скрипта.
**check_script_status** запускает скрипт из check с переданными параметрами. Ждет OK в ответ.
**check_process_status** проверяет наличие процесса.
У функции есть аргумент **priorities**, который отвечает за уровень проблемы. Возможные вариант: INFO, WARNING, AVERAGE, HIGH, DISASTER, CRITICAL. По умолчанию WARNING.
**description** содержит текст аварии. В нем можно указать переменную {ITEM.LASTVALUE1}, которая будет заменена на последнее полученное значение.
Аргумент **service** нужен для разметки события в juggler и для организации зависимостей в zabbix. В аргументе **depends_on_host_services** можно указать список **service** от которых будет зависеть проверка.
Пример:
```python
check1 = check_process_status(fqdns, proc_name="service1", service="service1", description="service1 is not running")
check2 = check_process_status(fqdns, proc_name="service2", service="service2", description="service1 is not running")
```
Аргумент **tag** опциональный и используется для свертывания событий в heat.

Синхронизация проверок запускается каждый час в 8 минут. Статус запуска в [juggler](https://juggler.yandex-team.ru/raw_events/?query=host%3Dznoc_master%26tag%3Dlinkator3.py%26service%3Dmondata_linkator).
Запустить discovery самостоятельно можно выполнив:
```shell
cd noc
$ ya make packages/mondata_server/cmd/mondata_python
$ packages/mondata_server/cmd/mondata_python/mondata_python mondata/discovery/ike_daemon.py
```

### 2.1 Внести информацию о проблеме и пути её решения в вики
Необходимо в генераторе проверки указать аргумент ```help_key="слагаварии"``` чтобы в хите появилась ссылка вида "wiki/#слагаварии".
А [тут](https://wiki.yandex-team.ru/noc/duty/tipy-avarijj-v-heat/) добавить параграф, аналогичный предыдущим, с заголовком состоящим из "слаг аварии". Можно явно указать якорь в виде ```===(anchor) слаг аварии===```, требования к якорю - нельзя использовать пробелы, подчеркивания и т.д. Только латинские буквы и цифры.


### Как отлаживать проверку
mondata тащит с собой окружение со всеми нужными зависимостями, в не ставит их в систему. Поэтому нужно указать путь до окружения так:
```bash
 PYTHONUSERBASE=/var/spool/mondata/virtualenv/amd64/ python3 my_check.py
```
Либо указать путь до virtualenv в рабочей копии проекта mondata.

Zabbix запускает все скрипты через wrapper.py. Он следит за таймаутам,
запускает в фоне, пересылает и жагглер результат и прочее. Каждый его запуск логгируется в /var/log/zabbix/wrapper.py.log.
В дебаге виден и результат проверки и что было отослано в жагглер.
```shell
$ /var/spool/mondata/check/wrapper.py -d slbcloghandler.sh
2021-03-24 14:25:08,685 __main__ - wrapper.py:483 - main() - DEBUG - cmd args: Namespace(background=False, cmd='slbcloghandler.sh', cmdargs=[], debug=True, debug_log_file=False, juggler=True, juggler_wrapper=None, no_juggler=False, resp=None, syslog=True, template='%s', timeout=20)
2021-03-24 14:25:08,686 __main__ - wrapper.py:243 - command() - DEBUG - run cmd='/var/spool/mondata/check/slbcloghandler.sh' args=[] timeout=20 env={'PATH': '/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin', 'HOME': '/home/zabbix'}
2021-03-24 14:25:08,710 __main__ - wrapper.py:269 - command() - DEBUG - cmd='/var/spool/mondata/check/slbcloghandler.sh' args=[] returned code=0 out='PASSIVE-CHECK:slbcloghandler_alive;0; Ok\nPASSIVE-CHECK:slbcloghandler_ping;0; Ok' err=''
2021-03-24 14:25:08,717 __main__ - wrapper.py:126 - send_to_juggler() - DEBUG - send to juggler [{'service': 'slbcloghandler_alive', 'description': ' Ok', 'status': 'OK', 'tags': ['mondata_wrapper_result', 'slbcloghandler.sh'], 'host': 'iva-sch1.net.yandex.net'}, {'service': 'slbcloghandler_ping', 'description': ' Ok', 'status': 'OK', 'tags': ['mondata_wrapper_result', 'slbcloghandler.sh'], 'host': 'iva-sch1.net.yandex.net'}, {'description': 'slbcloghandler.sh res:  ', 'service': 'mondata_check_slbcloghandler.sh', 'host': 'iva-sch1.net.yandex.net', 'status': 'OK', 'instance': '', 'tags': ['mondata_check_error', 'slbcloghandler.sh']}]
2021-03-24 14:25:09,337 root - wrapper.py:134 - send_to_juggler() - DEBUG - sent data to url=http://juggler-push.search.yandex.net:80/api/1/batch
PASSIVE-CHECK:slbcloghandler_alive;0; Ok
PASSIVE-CHECK:slbcloghandler_ping;0; Ok
```

Чтобы проверить что в заббикс приехали настройки проверки, идем в https://znoc.yandex-team.ru, находим свой хост в поиске, убеждаемся что в Items есть ваш скрипт.

### Передать проверку дежурной смене
Любую новую проверку требуется передать дежурной смене NOC. Процедура описана на странице https://wiki.yandex-team.ru/users/ilysogor/monitoring-acceptance/#kakperedatalertilipanel


### Хранение паролей
Проверки типа external (выполняемые на сервере мониторинга), можно хранить в [секретнице](https://yav.yandex-team.ru/secret/sec-01cxfm7wgbxj07cc4bbjs1qbbq).
Для этого нужно добавить в секретницу свой пароль, а в проверке получить пароль так:
```python
from lib.lib import get_password
password = get_password("my_pass_key")
```
На серверах заббикса, раз в час запускается автоматика, которая дергает пароли из секретицы с тегом "mondata". Кроме тега, для того чтобы автоматика получила пароль, надо дать права на чтения для robot-znoc.
Для того чтобы потестировать скрипты, нужно у себя в домашней папке сделать файл vault_keys с json'ом вида:
```json
{"my_pass_key": "password", "my_pass_key2": "password2"}
```

### Обновление пакета:

### Ручное обновление
#### Linux:
Создать файл /etc/apt/sources.list.d/noc_stable_dist_yandex_ru_noc.list.list содержаший строку "deb http://noc.dist.yandex.ru/noc stable/all/". И выполнить:
```bash
apt-get update
apt-get install mondata
```
#### FreeBSD
Если хост не noc-*:
```bash
pkg update -f
pkg install -y mondata
```
Если noc, то:
```bash
make -C /usr/ports/local/mondata update clean reinstall
```


### Удаление discovery
Автоматика удаляет результат парсинга, но если долго из заббикса не уезжает проверка, то есть смысл проверить что файл с результатом удален из https://a.yandex-team.ru/robots/trunk/nocdev/mondata_configs

### Утилита checks_info.py
Утилита сделана в помощь для выгрузки данных по проверкам в Discovery.
Для использования нужно склонировать к себе mondata и установить зависимости requirements.txt
На вход нужно подать `username` для чекаута mondata_configs из Arcadia.
NOTE: первый запуск будет продолжительный из-за чекаута конфигов, последующие быстрее.
Утилита позволяет:
- с флагом `--device DEVICE` выгрузить по имени хоста все проверки, которые используются на хосте
- с флагом `--predicate "PREDICATE"` выгрузить все проверки использующиеся на хостах в указанном предикате
- с флагом `--check "discovery_script.py"` выгрузить все хосты, которые попадают в проверку из папки discovery
- с флагом `--print_groups` выводит сгруппированные проверки по хостам (возможно полезно для создания Кулебяк)

__Пример использования:__
```bash
(.venv) alexprokhorov@alexprokhorov-x: python checks_info.py -u alexprokhorov -p "{сервер RT}"
Checks on devices in {сервер RT}:
        -  agent_ping.py
        -  certcheck.py
~omit~
        -  unreachable.py
        -  zabbix_agent.py
===
Devices in {сервер RT} but without Checks:
        -  myt-rt1.net.yandex.net
        -  sas-rt1.net.yandex.net
        -  vla-rt1.net.yandex.net

(.venv) alexprokhorov@alexprokhorov-x: python checks_info.py -u alexprokhorov -d man1-rt1
Checks on man1-rt1:
        -  agent_ping.py
        -  certcheck.py
~omit~
        -  unreachable.py
        -  zabbix_agent.py

(.venv) alexprokhorov@alexprokhorov-x: python checks_info.py -u alexprokhorov --check juniper_alarms.py
Hosts in discovery_check juniper_alarms.py
        - myt-b3.yndx.net
        - sas-61d1.yndx.net
        ~omit~
        - myt-b1.yndx.net
        - sas-85d3.yndx.net
Total Devices: 94

(.venv) alexprokhorov@alexprokhorov-x:python checks_info.py -u alexprokhorov -pg
['nexus_ra_check.py.json', 'nocauth.py.json', 'switch_mgmt.py.json', 'unreachable.py.json']
['man1-s334.yndx.net']

['nocauth.py.json', 'snmp.py.json', 'switch_mgmt.py.json', 'unreachable.py.json']
['sas1-i672.yndx.net', 'sas1-i535.yndx.net', ~omit~ 'sas1-i712.yndx.net']

['nocauth.py.json', 'snmp.py.json', 'unreachable.py.json']
['man-20x7.yndx.net', 'vla-20x3.yndx.net', ~omit~, 'vla-39d4.yndx.net']

['pinger.py.json']
['taxi-myt-mon', 'taxi-sas-mon', 'taxi-myt-graylog']

['snmp.py.json', 'switch_mgmt.py.json']
['myt-s24.yndx.net', 'myt-s697.yndx.net', ~omit~, 'cipt-ash-vm3.yndx.net']

['juniper_alarms.py.json', 'nocauth.py.json', 'snmp.py.json', 'unreachable.py.json']
['std-6pe.yndx.net', 'kiv-6pe.yndx.net']

['juniper_alarms.py.json', 'nocauth.py.json', 'switch_mgmt.py.json', 'unreachable.py.json']
['man-0cp255.yndx.net', ~omit~, 'vla1-4cp1.yndx.net']

['juniper_alarms.py.json', 'nocauth.py.json', 'unreachable.py.json']
['std-lurr1.yndx.net']

['juniper_alarms.py.json', 'snmp.py.json', 'switch_mgmt.py.json']
['man-32z9.yndx.net', 'qfx5210-64c-test1.yndx.net', 'vla-16d1.yndx.net', 'man-32z7.yndx.net', 'qfx5210-64c-test2.yndx.net', 'man-32z8.yndx.net']

['juniper_alarms.py.json', 'switch_mgmt.py.json', 'unreachable.py.json']
['netlab-sas2-92cp255.yndx.net']

['juniper_alarms.py.json', 'switch_mgmt.py.json']
['lab-m9-b1.yndx.net']

['juniper_alarms.py.json']
['qfx5200-test.yndx.net']
```

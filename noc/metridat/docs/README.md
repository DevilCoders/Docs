### Huawei telemetry
Список поддерживаемых путей подписки можно посмотреть командой ```display telemetry sensor-path```. Скорей всего там не весь список.\
Пример вывода:
```<lab-vla-32z5>display telemetry sensor-path
------------------------------------------------------------------------------------------------------------------
Type          MinPeriod(ms)  MaxEachPeriod  Path
------------------------------------------------------------------------------------------------------------------
Sample        1000           --             huawei-debug:debug/cpu-infos/cpu-info
Sample        1000           --             huawei-debug:debug/memory-infos/memory-info
Sample        300000         --             huawei-devm:devm/ports/port/huawei-pic:ethernet/fec-error-statistics
Sample        1000           --             huawei-ifm:ifm/interfaces/interface
Sample        100            20             huawei-ifm:ifm/interfaces/interface/common-statistics
OnChange+     --             --             huawei-ifm:ifm/interfaces/interface/dynamic/oper-status
OnChange+     --             --             huawei-ifm:ifm/interfaces/interface/dynamic/physical-status
Sample        10             100            huawei-ifm:ifm/interfaces/interface/mib-statistics
Sample        100            20             huawei-qos:qos/global-query/interface-traffic-policy-statisticss/interface-traffic-policy-statistics/rule-based-staticss/rule-based-statics
Alarm         --             65535          huawei-routing-notification:ipv4-prefix-exceed
Sample        1000           120            other paths
```
[Документация](https://support.huawei.com/enterprise/en/doc/EDOC1100139551/ca35df87/about-this-document) от Huawei.

В зависимости от модели может потребоваться лицензия.

Модель | Лицензия
--- | ---
NE40E | This feature is a basic feature and is not under license control
8800 and 6800 | Telemetry is under license control
[Про лицензии](https://support.huawei.com/enterprise/en/doc/EDOC1000060766/807e2e9d/what-features-are-licensed-on-ce-series-switches)
###
В stable перенести можно так:
```shell
ssh noc.dupload.dist.yandex.ru
find_package -e unstable metridat | grep _amd64.deb
sudo dmove noc stable metridat-client 1.8.xxx unstable
sudo dmove noc stable metridat-server 1.8.xxx unstable
```

Группа [conductor](https://c.yandex-team.ru/groups/nocdev-metridat-collector) \
Выкатка:
```shell
executer p_exec %nocdev-metridat-client "salt-call state.highstate"
executer p_exec %nocdev-metridat-server "salt-call state.highstate"
executer p_exec %nocdev-metridat-client "apt-get install metridat-client"
executer p_exec %nocdev-metridat-server "apt-get install metridat-server"
```
Группа [conductor](https://c.yandex-team.ru/groups/nocdev-metridat-client)

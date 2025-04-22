**Gfglister** - сервис для синхронизации конфигурации с устройства в VCS.
Gfglister получает сигнал об изменении конфигурации от разных источников:
SNMP trap от [snmptrapper](https://a.yandex-team.ru/arc/trunk/arcadia/noc/snmptrapper),
syslog от [metridat-aggregator](https://a.yandex-team.ru/svn/trunk/arcadia/noc/metridat/docs/README_AGGREGATOR.md)
и просто через http ручку.
Полученный конфиг сохраняется в роботную аркадию (svn+ssh://arcadia.yandex.ru/robots/trunk/noc/cfglister/gfglister_config [WebSVN](https://arc.yandex-team.ru/wsvn/robots/trunk/noc/cfglister/config)) через SVN.
В комментарий к коммиту конфига подмешивается информация об авторстве, если её удалось получить.
Основной потребитель конфигов checkist и аннушка.

Список хостов обслуживаемых сервис ограничен предикатом [[работает gfglister]](https://racktables.yandex-team.ru/index.php?andor=and&cfe=%5Bработает+gfglister%5D&page=depot&tab=default).

Схема сервиса:
[<img src="https://jing.yandex-team.ru/files/gescheit/gfglister3.jpg" width="1000"/>](https://jing.yandex-team.ru/files/gescheit/gfglister.jpg)

Текущий статус сервиса:
<iframe height="800" width="100%" frameborder="0" src="https://monitoring.yandex-team.ru/embed/gfglister/dash/monm6ts2h94f5e7h5qoh?from=now-120m&to=now"></iframe>

# dev-proxy
Прокси, позволяющая использовать на деве произвольные front и back

## Сборка
Для precise - ручная, для xenial - в teamcity https://teamcity.yandex-team.ru/viewType.html?buildTypeId=PortalAkaMordaProjects_PortalMordaXenial_DevProxy

## Выкладка
Автоматически на девы через кондуктор

## Как запустить, остановить
`sudo (start|restart|stop) dev-proxy`

## Как настроить дев для разработки dev-proxy
0. Добавить свой дев в configurator/configurator.conf
1. `make conf`
2. Сконфигурировать морду с флагами **proxified** и **devproxy**
3. запуск-перезапуск `sudo (start|restart) dev-proxy-<instance>`

Логи в `/var/log/dev-proxy/error-<instance>.log`

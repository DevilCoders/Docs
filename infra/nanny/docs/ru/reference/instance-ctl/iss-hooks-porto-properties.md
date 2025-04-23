# Porto-свойства ISS-хуков

##  Используемые ISS-хуки {#hooks}
Весь список хуков, поддерживаемых `instancectl` (взято [отсюда](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/instancectl/iss_hooks)) можно разделить на 2 категории:
Хуки, которые не могу работать параллельно друг с другом (т.е. в один момент времени работает только один из):

* `iss_hook_start`
* `iss_hook_install`
* `iss_hook_uninstall`
Хуки, выполняющиеся параллельно с другими:
* `iss_hook_stop`
* `iss_hook_status`
* `iss_hook_reopenlogs`
* `iss_hook_notify`

##  Иерархия контейнеров ISS {#iss-hierarchy}
Все ISS-хуки инстанса запускаются в мета-контейнере на одном уровне иерархии:

```
ISS-AGENT--11113_test_service_3_1ATYK0cDDIN  # metacontainer
├── iss_hook_{start,install,uninstall}
├── iss_hook_status
├── iss_hook_stop
├── iss_hook_notify
└── iss_hook_reopenlogs
```
##  Особенности запуска с MTN со слот-контейнером {#net-slot}
1. Сеть навешивается на slot-контейнер, в `network namespace` слота запускаются `iss_hook_{start,install,uninstall}`;
1. Остальные хуки запускаются в `net: none`.

##  Особенности запуска с SANDBOX_LAYERS {#sandbox-layers}
1. Все хуки запускаются в `virt_mode: app`.

##  Особенности запуска с Docker-образом {#docker}
Ниже приведены особенности запуска инстанса с docker-образом.

1. В docker-образах все файлы имеют root в качестве owner'а.
Поэтому все хуки инстанса должны также быть запущены из-под root. Это касается всех хуков, в том числе запускаемых параллельно с `iss_hook_start` из-за [SWAT-3356](https://st.yandex-team.ru/SWAT-3356).
1. Мы не можем использовать porto-свойства `user: root, group: root`, т.к. ISS-agent запускается из-под `loadbase`, а porto2 не позволяет выставлять эти свойства если процесс, создающий контейнер, выполняется не из-под `root`.
1. Поэтому в качестве workaround мы используем `virt_mode: os`.
1. Porto запускает контейнеры в `virt_mode: os` с избыточным списком capabilities для части хуков. Нужно запускать хуки, выполняющиеся параллельно с `iss_hook_start` с урезанным набором capabilities, т.к. единственное, что они должны делать -- это дёрнуть метод instancectl через unixsocket.

##  Дерево принятия решений {#trees}
###  Выбор virtmod {#trees-virt-mode}
```
                 +-------------------------+
                 |                         |
                 |     Тип инстанса        |
                 |                         |
                 +-----+------+-------+----+
                       |      |       |
                       |      |       |
                       |      |       |
          DOCKER_LAYERS|      |       |SANDBOX_LAYERS
         +-------------+      |       +------------+
         |                    |                    |
         |                    |                    |
         |                    |Legacy              |
+--------+------+             |             +------+---------+
|  All hooks:   |             |             |   All hooks:   |
| virt_mode: os |             |             | virt_mode: app |
+---------------+      +------+---------+   +----------------+
                       |   All hooks:   |
                       | virt_mode: app |
                       +----------------+
```
###  Настройка сети для `iss_hook_start` {#trees-iss-hook-start-net}
```
                                       +--------------+
                                       |              |
                                       |   Use MTN    |
                                       |              |
                                       +---+-----+----+
                                           |     |
                                    True   |     |   False
                                 +---------+     +----------+
                                 |                          |
                        +--------v-------+          +-------+---------------------+
                        | Slot containers|          |iss_hook_start.net: inherited|
                        |  are in prod?  |          +-----------------------------+
                        +----+------+----+          
                             |      |
                             |      |
                       Yes   |      |   No
                    +--------+      +-------+
                    |                       |
                    |                       |
+-------------------+----------+     +------v--------------------+
|slot.net: L3 veth             |     |                           |
|slot.ip: veth ...             |     |iss_hook_start.net: L3 veth|
|iss_hook_start.net: inherited |     |iss_hook_start.ip: veth ...|
+------------------------------+     +---------------------------+

```
###  Настройка сети остальных хуков {#trees-other-hooks-net}
```
                          +-------------------------+
                          |                         |
                          |     Тип инстанса        |
                          |                         |
                          +-----+------+-------+----+
                                |      |       |
                                |      |       |
                                |      |       |
                   DOCKER_LAYERS|      |       |SANDBOX_LAYERS
                  +-------------+      |       +------------+
                  |                    |                    |
                  |                    |Legacy              |
                  |                    |                    |
+-----------------+---------------+ +--+--------------------+----------+
|iss_hook_install.net: inherited  | |iss_hook_install.net: inherited   |
|iss_hook_uninstall.net: inherited| |iss_hook_uninstall.net: inherited |
|iss_hook_stop.net: none          | |iss_hook_stop.net: inherited      |
|iss_hook_status.net: none        | |iss_hook_status.net: inherited    |
|iss_hook_reopenlogs.net: none    | |iss_hook_reopenlogs.net: inherited|
|iss_hook_notify.net: none        | |iss_hook_notify.net: inherited    |
+---------------------------------+ +----------------------------------+
```
##  Список всех вариантов porto-свойств {#table}
Легенда:

* `LEGACY` - контейнеры запущены без изоляции по network и mount namespace.
* `DOCKER` - контейнеры запущены с rootfs из образа Docker.
* `SANDBOX_LAYERS` -контейнеры запущены с rootfs из ресурсов Sandbox.

Тип инстанса | Есть slot-контейнер | MTN | virt_mode | start.net | [un]install.net | parallel_hook.net | slot.net | slot.limits
:--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :---
LEGACY | ✓ | ✓ | app | inherited | inherited | none | veth | ✓
LEGACY | ✓ |  | app | inherited | inherited | inherited | inherited | ✓
LEGACY |  | ✓ | app | veth | inherited | none | inherited | 
LEGACY |  |  | app | inherited | inherited | inherited | inherited | 
DOCKER | ✓ | ✓ | os | inherited | inherited | none | veth | ✓
DOCKER | ✓ |  | os | inherited | inherited | none | inherited | ✓
DOCKER |  | ✓ | os | veth | inherited | none | inherited | 
DOCKER |  |  | os | inherited | inherited | none | inherited | 
SANDBOX_LAYERS | ✓ | ✓ | app | inherited | inherited | none | veth | ✓
SANDBOX_LAYERS | ✓ |  | app | inherited | inherited | inherited | inherited | ✓
SANDBOX_LAYERS |  | ✓ | app | veth | inherited | none | inherited | 
SANDBOX_LAYERS |  |  | app | inherited | inherited | inherited | inherited | 

##  Необходимые доработки {#next-steps}
1. Запрет запуска кастомных хуков без instancectl под docker: [https://st.yandex-team.ru/SWAT-3267](https://st.yandex-team.ru/SWAT-3267)
1. Ограничить capabilities для хуков, выполняющихся параллельно с iss_hook_start: [https://st.yandex-team.ru/SWAT-3159](https://st.yandex-team.ru/SWAT-3159)


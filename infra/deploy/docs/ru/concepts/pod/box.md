# Box

**Box** — это контейнер, файловая система, docker образ, porto слои. В Box указываются ограничения по ресурсам, общие для [Workload](workload/workload.md) переменные окружения, базовые слои вашего приложения (docker/porto), статические и динамические ресурсы. Другими словами, именно в Box мы определяем файлы, запуск которых настраивается в Workload'ах.

Box обозначается значком ![box-icon](../../_assets/icons/box.png).

## Описание

Обеспечивает изоляцию по mount/pid/ipc/utc/env ns.
Транслируется в `porto volume` + `porto meta container` (контейнер без команды запуска).

Сеть между боксами не изолирована - workload'ы разных боксов могут общаться друг с другом по localhost:

```bash
$: ssh -6 root@2a02:6b8:c0a:40c0:0:696:dfe5:2  # ssh to logbroker_tools_box
root@man2-9244-1:/# curl localhost:80  # call to workload at yanddmi-test-stage-box-0
Hello my dear @yanddmi!
```

Также для связи боксов можно создать общий [volume](volume.md), примонтированный к нескольким боксам.

Боксы обновляются независимо друг от друга (если в новой ревизии не изменились ресурсы/вольюмы, от которых зависят оба бокса).

Если у вас есть некое "сайдкар"-приложение (workload), которое хочется обновлять независимо от "основного", можно выделить для него отдельный бокс.
Например, каждый из инфраструктурных "сайдкаров" типа logbroker или tvmtool запускается в своем боксе. Раскатка релиза нового бинарника logbroker не аффектит пользовательские боксы/приложения.

В Деплое слой представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5791549#L521-571):

##  Слои и ресурсы

В бокс можно принести ресурсы двух типов: layers и static resources.

Бокс собирается из слоев.

Слои должны содержать "базовый" образ ОС. Можно использовать [стандартные базовые образы](https://wiki.yandex-team.ru/runtime-cloud/virtualimages/), подготовленные командой SRE.

Docker образы также поддерживаются - [на верхнем уровне абстракции - в объекте stage](../stage/ispolzovanie-docker-obraza.md)

Слои наслаиваются **справа налево**, т.е. первый слой в списке будет наложен последним. Так сделано чтобы соответствовать `api porto`: `layers - layers, syntax: top-layer;...;bottom-layer`
(семантика из overlayfs: файл вначале ищется в первом слое, если там нет то во втором слое, и т.д.)

После сборки слоев к боксу монтируются static resources.
Static resource нельзя монтировать в / бокса.
Static resource одного бокса не могут пересекаться по точкам монтирования.

Например:

```yaml
resources:
  layers:
  - id: logbroker_base_layer
    checksum: MD5:234a033db29f2e4afae189851c0ee63d
    url: rbtorrent:edd2795d2d7674eae43c4ad0de3dad563be11f94
  - id: logbroker_tools_layer
    checksum: 'EMPTY:'
    url: rbtorrent:e246968a4997da89df20fe064c0062ce3033092b
  static_resources:
  - id: push_agent_config
    url: raw:{"port":2222,"mon_port":12501}
    verification:
      checksum: 'EMPTY:'
boxes:
- id: logbroker_tools_box
  compute_resources:
    anonymous_memory_limit: 536870912
    memory_limit: 536870912
    vcpu_limit: 400
  rootfs:
    layer_refs:
    - logbroker_tools_layer
    - logbroker_base_layer
  static_resources:
  - mount_point: static_data
    resource_ref: push_agent_config
```

## Персистентность

Данные будут потеряны, если:

* pod переезжает на другой хост
* (или) спека бокса изменилась
* (или) зависимости бокса (слои/ресурсы) изменились

В остальных случаях данные сохраняются.
Например, данные сохранятся в кейсах:

* выкатка zero-diff
* смена workload.cmd (или CMD в Dockerfile)

Для задач персистентности также можно использовать [volume](volume.md).

##  Переменные окружения

Переменные окружения прокидываются во все init контейнеры бокса и во все вложенные workload
При этом, если переменная окружения указана и в box env, и в workload env, то будет выбрано значение из workload env
Пример:

```yaml
boxes:
- id: logbroker_tools_box
  compute_resources:
    anonymous_memory_limit: 536870912
    memory_limit: 536870912
    vcpu_limit: 400
  rootfs:
    layer_refs:
    - logbroker_tools_layer
    - logbroker_base_layer
   env:
   - name: 'VERSION'
     value:
       literal_env:
         value: '0.1'
```

###  Init commands {#init}

Иногда недостаточно просто собрать `box` из разных ресурсов и `mount`'ов разных `volume`, и нужно сделать что-то дополнительное. Например, распаковать ресурс или принести данные, доступ до которых требует особую авторизацию.

Я.Деплой предоставляет возможность использовать `Init` команды для указания набора действий, которые будут выполнены перед тем, как бокс будет считаться готовым к работе.

По умолчанию, все команды запускаются в cwd - `/` box'а, но мы настоятельно рекомендуем указывать полный путь. Помимо этого, `Init` команды игнорируют домашнюю директорию из `/etc/passwd` и переменная окружения `$HOME` равна `/`. 

`Init` команды (последовательно) выполняются после создания структуры вольюмов, перед запуском ворклодов.

Во время выполнения команд `box` находится в состоянии `INIT_PROCESSES`.

Если одна из `Init` команд завершилась неуспешно, она перезапускается до того момента, пока результат не будет успешным [вот тут можно почитать подробнее](workload/probes.md#primer-ispolzovaniya).

После успешного завершения всех команд бокс переводится в состоянии `READY` - что значит, что в нем можно запускать workload's.

Обращаем внимание, что все `child` `Init` команды, после ее завершения, будут убиты (более точно, все соседи по `freezer cgroup`). Поэтому их нельзя использовать для запуска `self daemonize` процессов. Если вам нужен какой-то демон в контейнере, создайте отдельный `workload` и используйте [start команду](workload/workload.md#start).

```yaml
boxes:
- id: TestEnvAndInitBox
  ...
  env:
  - name: RSA_KEY
    value:
      secret_env:
        id: MyRsaKey
        alias: MyKeys
  - name: CONFIG_SERVER_ADDRESS
    value:
      literal_env:
        value: proxy.my_server.yandex-team.ru
  init:
  - command_line: /bin/bash -c 'mkdir -p ~/.ssh; echo -n $RSA_KEY > ~/.ssh/id_rsa'
  - command_line: /bin/bash -c 'rm -rf ~/config; mkdir ~/config; scp -r $CONFIG_SERVER_ADDRESS:/config_path/* ~/config'
    time_limit:
      min_restart_period_ms: 180000
      max_restart_period_ms: 180000
      max_execution_time_ms: 60000
  - command_line: ./patch_config.sh
```

## SSH в box

Доступ в box нужен для доступа к файловой системе компонента сервиса.

У каждого бокса есть свой IP-адрес, который используется специально для SSH-доступа к нему.
Чтобы попасть в файловую систему бокса, надо использовать `ssh root@HOST`, где **HOST** — это IP-адрес или DNS-имя бокса из UI.

##  Запись секрета в переменную окружения

Предварительно необходимо [добавить секрет и delegation_token](../../reference/tools/dctl.md#delegation-token) в спеку RS/MCRS.

Для записи секрета в файл надо объявить env с опцией secret_env:

```yaml
boxes:
- id: box
  ...
  env:
  - name: MY_SECRET
    value:
      secret_env:
        alias: sec-01dhnpx1t7eahavh43dazfjqm9:ver-01dsfcgvnhr9vnwq844ep81vsx
        id: YANDDMI_TEST_SECRET
  - name: MY_LITERAL
    value:
      literal_env:
        value: not_secret_value
```

##  Запись секретов в файл

Запись секретов в файл происходит [при помощи static resource](static-resources.md#secret).

После этого в боксе нужно указать ссылку на этот static resource:

```yaml
boxes:
- id: SomeBox
  ...
  static_resources:
  - resource_ref: TestFiles
    mount_point: secret_data
```

##  Системные переменные окружения {#systemenv}

В переменных окружения box доступна следующая информация (все эти переменные наследуются вложенными workload):

```bash
ПЕРЕМЕННАЯ                     = Пример реального значения # Описание

TVMTOOL_LOCAL_AUTHTOKEN        = <MD5 hash>  # Токен для использования tvm tool, гарантированно добавляется всегда независимо от наличия tvm box, эту переменную нельзя override'ить
DEPLOY_TVM_TOOL_URL            = http://localhost:32272 # Адрес для использования tvm tool, есть только при наличии tvm tool box

DEPLOY_PROJECT_ID              = project_id
DEPLOY_STAGE_ID                = stage_id
DEPLOY_UNIT_ID                 = deploy_unit_id
DEPLOY_BOX_ID                  = box_id

DEPLOY_NODE_CLUSTER            = sas.yp.yandex.net # fqdn мастера yp, ибо кластер yp может не соответствовать DC, где находится нода
DEPLOY_NODE_DC                 = sas # DC в котором находится нода, может не соответствовать yp кластеру, ибо, например, на sas-test есть ноды из iva
DEPLOY_NODE_FQDN               = sas3-5315.search.yandex.net

DEPLOY_POD_ID                  = vwwxmnw3w5amfq2v
DEPLOY_POD_PERSISTENT_FQDN     = vwwxmnw3w5amfq2v.sas.yp-c.yandex.net
DEPLOY_POD_TRANSIENT_FQDN      = sas3-5315-1.vwwxmnw3w5amfq2v.sas.yp-c.yandex.net

DEPLOY_POD_IP_0_ADDRESS        = 2a02:6b8:c1b:2783:0:696:19a6:0
DEPLOY_POD_IP_1_ADDRESS        = 2a02:6b8:fc1c:2783:0:696:72ee:0
...
DEPLOY_POD_IP_<NUMBER>_ADDRESS = <ip>
```

Обратите внимание, что префикс `DEPLOY_` зарезервирован для переменных окружения, выставляемых системно

Список и связь с runtime version в  [документе](https://deploy.yandex-team.ru/docs/reference/environment-variables)

##  Хостовый skynet

Атрибут `TBox.bind_skynet` [https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5703927#L518](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5703927#L518)

Если указано true, pod agent создает bind volume из `<pod_chroot>/place/berkanavt/supervisor` в `<box_chroot>/place/berkanavt/supervisor`

На файловой системе box'а обязательно наличие директории /place/berkanavt/supervisor и следующих симлинков (без них скачивание/раздача работать не будут совсем):

* /skynet => /Berkanavt/supervisor/base/active
* /usr/local/bin/sky => /skynet/tools/sky
* /Berkanavt => /place/berkanavt

Эти директории и симлинки можно добавить с помощью небольшого слоя [sbr:922226367](https://sandbox.yandex-team.ru/resource/922226367/view)

Если вы используете расширенные базовые образы, нужные симлинки в них [уже есть](https://wiki.yandex-team.ru/runtime-cloud/virtualimages/#rasshirennyjjobraz)

В UI включить опцию `TBox.bind_skynet` можно в новом конфиге на странице редактирования бокса:

### Сетевые доступы для skynet

Для cqudp (sky run): если вы планируете запускать sky run на хостах в подсети с именем `_SOURCE_NETS_`, а контейнеры сервиса запущены в подсети `_DESTINATION_NETS_`, необходимо получить следующие доступы в [Puncher](https://puncher.yandex-team.ru/):

- from `_SOURCE_NETS_` to `_DESTINATION_NETS_` udp port 10040,10041,32000-65535
- from `_DESTINATION_NETS_` to `_SOURCE_NETS_` udp port 32000-65535

##  Подключение NAT64 (в box и всех вложенных в него workload)

Чтобы ходить во внешние IPv4-only сервисы из контейнеров используется технология [NAT64](https://en.wikipedia.org/wiki/NAT64). Для включения:

* Указываем в настройках box'а опцию `resolv_conf: "nat64_local"` (в UI - блок `resolv.conf`).
* Запрашиваем доступ из вашей сети до Интернет в [https://puncher.yandex-team.ru/,](https://puncher.yandex-team.ru/,) в качестве приёмника нужно указать слово `Интернет`.
* Используем [Runtime version 5](../../reference/patchers-revision#runtime-version-5) или выше

После включения этой опции в `/etc/resolv.conf` в box в качестве nameserver будут указаны адреса DNS сервисов, поддерживающие трансляцию IPv4 в IPv6.

Пример спеки для dctl:

```yaml
boxes:
- id: "box"
  ...
  resolv_conf: "nat64_local"
```

**Важно:** опцию __NAT64__ использовать **не рекомендуется**, она оставлена для обратной совместимости и в будущем будет удалена.

## Хождение в во внешний интернет через IPv6
Во внутренней сети используется jumbo frame, это может быть проблемой при походе во внешний интернет через IPv6
Для понижения MTU можно использовать параметр [extra_routes](https://a.yandex-team.ru/svn/trunk/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r8578031#L1652)


##  Создание tmpfs

Для создания tmpfs вольюма в боксе должна присутствовать утилита portoctl.
Утилита установлена в расширенных (*-os) базовых образах.

Добавьте init скрипт:

```bash
bash -c '
if [ ! -d /tmpfs ]; then
    mkdir /tmpfs
    portoctl vcreate /tmpfs backend=tmpfs space_limit=64M
fi
'
```

##  Граф состояний

![box](../../_assets/concepts/pod/box/box.png)
![legend](../../_assets/legend.png)

##  cgroupfs
**Что это:**
Возможность получать данные о ресурсах контейнера из cgroupfs

**Как включить:**
UI:

![в разделе редактирования Box](https://jing.yandex-team.ru/files/amich/cgroupfs2.png)

dctl:
[спецификация](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/stage.proto?rev=9709368976789150745deccc5fac0cc79f560ea9#L173)

```
pod_template_spec:
  spec:
  ...
  pod_agent_payload:
    spec:
      boxes:	                 
        - cgroup_fs_mount_mode: "ro"
          id: "box"
   ...                  
```


**Как это работает:**
в контейнер монтируется виртуальная файловая система, где можно прочитать доступную память и cpu
если на Box лимиты не заданы - будут отображаться лимиты Pod*
Эту возможность можно использовать с: 
* Java [подробный пост](https://clubs.at.yandex-team.ru/infra-cloud/2135) 
* C++,GO с использованием библиотек [Подробный пост](https://clubs.at.yandex-team.ru/infra-cloud/2211)

```*``` начиная с [Runtime version 11](../../reference/patchers-revision#runtime-version-11)

**Кому это не подойдет:**
Если ваш Pod/Box использует меньше 2х ядер, потенцеально могут возникнуть проблемы с оптимизациями параллельных стримов, пулов итд.
Если вам нужно точно количество физических ядер, VCPU - это "попугаи", которые пересчитываются при помощи benchmark для каждой модели CPU

### Виртуальный диск бокса {#virtual-disk-ref}

В случае, если у вас больше одного диска, необходимо указать `virtual_disk_id_ref`, чтобы файловая система бокса создалась на определенном диске. Данный `virtual_disk_id_ref` должен совпадать с аналогичным полем в леерах, вольюмах, статических ресурсах, которые линкуются к этому боксу. Иначе спека не пройдет валидацию.

```yaml
boxes:
- id: "box"
  ...
  virtual_disk_id_ref: disk-0
```

[Пример полной спеки с использованием нескольких дисков.](https://deploy.yandex-team.ru/docs/concepts/pod/diskvolumerequests#primer-speki-s-ispolzovaniem-neskolkih-diskov)



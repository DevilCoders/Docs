# Porto quickstart

PORTO - система управления контейнерами linux:
* [wiki](https://wiki.yandex-team.ru/porto/)
* [man](https://bb.yandex-team.ru/projects/PORTO/repos/porto/browse/porto.md)

Основная цель - предоставить единую точку входа для нескольких подсистем Linux, таких как cgroups, namespaces, mounts, nets и т.д.

## Примеры

### Запустить команду foreground:
```
$ portoctl exec hello command='echo "Hello, world!"'
```

### Запустить команду background:
```
$ portoctl run stress command='stress -c 4' memory_limit=1G cpu_limit=2.5c
$ portoctl destroy stress
```

### Создать вольюм и уничтожить:
```
$ mkdir volume
$ portoctl vcreate $PWD/volume space_limit=1G
$ portoctl vlist -v $PWD/volume
$ portoctl vunlink $PWD/volume
$ rmdir volume
```

>Volume - логическая файловая система под управлением порто - директория и файловое поддерево.
>Поведение, интерпретация параметров зависят от конкретной реализации (backend).
>Один или более контейнеров могут имеют ссылку на вольюм. При удалении последней ссылки вольюм уничтожается. По умолчанию контейнер создавший вольюм линкуется с ним.
>Данные вольюма доступны по пути указанном при создании (path). Каждая ссылка с контейнера может задавать дополнительный путь к вольюму внутри этого контейнера (target path).
>Вольюм адресуется любым из этих путей. В зависимости от бакэнда вольюм может ограничивать суммарный размер и число файлов или резервировать их в рамках place.
>Вольюм может хранить данные во временном или персистентном хранилище в place, ссылаться на внешний источник, использовать данные из слоёв хранящихся в том-же place или в пользовательских директориях.


### Создать вольюм с автоматическим выбором пути и уничтожить:
```
$ VOLUME=$(portoctl vcreate -A space_limit=1G)
$ portoctl vunlink $VOLUME
```

### Запустить virt_mode=os контейнер и зайти в него:

* virt_mode - режим виртуализации:
>
  * app - (по умолчанию) запуск команды как обычный процесс
  * os - запуск команды как init process
    Side effects of virt_mode=os
    * по умолчанию command="/sbin/init"
    * по умолчанию user="root", group="root"
    * по умолчанию stdout_path="/dev/null", stderr_path="/dev/null"
    * по умолчанию net=none
    * по умолчанию cwd="/"
    * доступна systemd cgroup если /sbin/init - systemd
    * команда stop посылает SIGPWR а не SIGTERM
  * host - команда запуска без ограничений безопасности
  * job - запуск процесса в сигруппах родительского контейнера
  * docker - запуск процесса в user namespace
    Side effects of virt_mode=docker
    * по умолчанию command="bash -c 'containerd& dockerd'"
    * создаются user и network неймспейсы
    * user и group не должны быть "root"
    * родительский контейнер должен быть с virt_mode="os"


>Слой(layer) - дерево файлов используемое при сборке вольюмов. Вольюм может использовать несколько слоёв одновременно — при поиске файлов имя ищется сначала в верхнем слое (upper layer, writable delta) которая хранится в сторадже вольюма, затем в первом слое, во втором и так далее.
В порто образ - готовый слой, в котором может подняться ос или любое приложение со всеми необходимыми либами и вспомогательными бинарями,
Слой хранится в place как immutable дерево файлов в формате [overlayfs](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt) и адресуется по имени.
Загрузка и выгрузка слоёв происходит через API в формате tarball архивов. Формат AUFS (использутеся в docker) при импортировании автоматически конвертируется в overlayfs.
Так-же вольюмы могут использовать слои из пользовательских директорий — в таком случае слой указывается полным путём до директории.
Готовые образы для RTC можно найти по [ссылке](./virtual-images.md).

* скачиваем [образ ubuntu-xenial](https://sandbox.yandex-team.ru/resource/1306122440/view)
```
$ sky get rbtorrent:f13e9fa0565c2da26eb72b318e5de1c31c26da50
```

* импортируем слой во внутреннее порто хранилище
```
$ portoctl layer -I ubuntu-xenial ubuntu-xenial.tgz
```

* создаем вольюм с автоматическим выбором пути, образом [ubuntu-xenial](https://sandbox.yandex-team.ru/resource/1306122440/view) и space_limit
```
$ sudo portoctl vcreate -A layers='ubuntu-xenial' space_limit=10G
/place/porto_volumes/1/volume
```

* запускаем контейнер с хостовой сетью
```
$ portoctl run abc virt_mode=os root=/place/porto_volumes/1/volume net=inherited
```

* зайдем в os контейнер
```
$ portoctl shell abc
```

* выходим
```
^D
```

* дестроим контейнер
```
$ portoctl destroy abc
```

* удаляем слой из порто хранилища
```
$ portoctl layer -R ubuntu-xenial
```


### Запуск докер демона в порто без CAP_SYS_ADMIN

* скачаем слои и импортируем в порто хранилище:
скачиваем слой [ubuntu-xenial](https://sandbox.yandex-team.ru/resource/1306122440/view)
```
$ sky get rbtorrent:f13e9fa0565c2da26eb72b318e5de1c31c26da50
```
 скачиваем слой [docker-xenial](https://sandbox.yandex-team.ru/resource/1801421485/view)
```
$ sky get rbtorrent:610c327cfcc04adeace4de8896d62db59ff53279
```

* импортируем в порто хранилище
```
$ portoctl layer -I ubuntu-xenial ubuntu-xenial.tgz
$ portoctl layer -I docker-xenial docker-xenial.tar.gz
```

* создадим вольюм с нужными слоями
```
$ portoctl vcreate -A layers='docker-xenial;ubuntu-xenial'
 /place/porto_volumes/1/volume
```

* запустим OS контейнер с хостовой сетью
```
$ portoctl run a virt_mode=os root=/place/porto_volumes/1/volume net=inherited
```

* зайдем в OS контейнер
```
$ portoctl shell a
```

* изменим владельца директорий в контейнере на не root
```
$ chown 1044.1044 /run
$ chown 1044.1044 -R /sys/fs/cgroup /var/lib/docker /var/lib/containerd /etc/docker /etc/containerd
```

* выйдем из OS контейнера
```
^D
```

*  и запустим подконтейнер с virt_mode=docker
>virt_mode=docker создает и настраивает user namespace, и у пользователя появляется CAP_SYS_ADMIN в этом пространстве имен, что позволяет запускать докер в привилегированном режиме]>
```
$ portoctl run a/b virt_mode=docker user=1044 group=1044 net='L3 veth' ip='veth auto'
```
>ip='veth auto'
автоматически берет ip с интерфейса vlan688.
Решение только для тестирования!

* зайдем через portoctl shell  в контейнер a  или a/b и запустим докер контейнер
```
$ docker run --privileged --net=host ubuntu
```

### Скачать докер образ из докер репозитория и сохранить как порто слой
#### Без использования докера
можно использовать [скрипт](https://a.yandex-team.ru/arc//trunk/arcadia/infra/porto/scripts/download-docker-image-in-porto-layer.sh), который по умолчанию скачивает образ из общего докер репозитория.
С опцией -rtc из репозитория https://registry.yandex.net, но это также требует [токен](https://wiki.yandex-team.ru/docker-registry/) в переменных окружения
#### С использованием докера

* запускаем докер контейнер (необходим для docker export)
```
$ docker run -d ubuntu
```

* сохраняем образ в tarball
```
$ docker export <container> -o layer.tar
```

* запускаем порто контейнер с полученным образом
```
$ portoctl exec -L layer.tar abc command=bash
```

### Расширенный запуск контейнера
[Готовые слои](./virtual-images.md), например возьмем слой [PORTO_LAYER_SEARCH_UBUNTU_XENIAL](https://sandbox.yandex-team.ru/resource/1932380113/view).

* скачаем его
  ```
  sky get rbtorrent:040050ed16cfe282f78ab3fd45058a7c80f79411
  ```

* импортируем слой в порто
  ```
  portoctl layer -I layer_name layer.tar.zst
  ```

* создаем [вольюм](https://wiki.yandex-team.ru/porto/disk/#volume) overlayfs с лимитом 1G:
  ```
  portoctl vcreate -A layers=layer_name space_limit=1G backend=overlay
  /place/porto_volumes/1/volume
  ```

* создадим контейнер:
  ```
  portoctl create container_name
  ```

* зададим чрут:
  ```
  portoctl set container_name root /place/porto_volumes/1/volume
  ```

* используем хостовую сеть:
```
net=inherited
```
>есть 3 вида сети
a) net=inherited - наследовать сеть родительского контейнера. Если запускается с хоста, нет изоляции по сети
b) [net="L3 veth"](https://wiki.yandex-team.ru/porto/network/#l3-in-container) удобна для создании изоляции по сети с хоста
быстрая настройка L3 сети(вариант только для тестирования, т.к. выделяет адрес в обход общих аллокаторов):
portoctl set container_name net 'L3 veth'
portoctl set container_name ip 'veth auto'
c) [net=NAT](https://wiki.yandex-team.ru/porto/network/#natdljakontejjnera) удобна для изоляции по сети в QYP виртуалках]>

* зададим net limit
```
portoctl set container_name net_limit '1K'
```
также можно отдельно задавать rx/tx лимиты

* зададим cpu_limut
```
portoctl set container_name cpu_limit 1.5c
```

* установим hostname
```
portoctl set container_name hostname 'contailer_host_name123456789.yandex.net'
```
>hostname - hostname внутри контейнера
Внутри чрута контейнера /etc/hostname должен быть обычным файлом, порто делает bind-mounts временный файл поверх него.

* зададим dns64
```
portoctl set container_name resolv_conf 'nameserver fd64::1'
```
>resolv_conf - DNS resolver configuration, default|keep|<resolv.conf option>;...
По умолчанию настройка resolv_conf="default" берет конфигурацию из portod.conf:
```
container {
    default_resolv_conf: "nameserver <ip>;nameserver <ip>;..."
}
```
или с хоста /etc/resolv.conf если опция в portod.conf отсутствует
Внутри чрута контейнера /etc/resolv.conf должен быть обычным файлом, порто делает bind-mounts временного файла поверх него.


* пробросим необходимые девайсы в контейнер
a) через свойство devices:
```
portoctl set container_name devices '/dev/nvidia1234 rw; /dev/nvidia567 rw'
```
b) через конфиг порто /etc/portod.conf
```
container {
    extra_devices: "<device> [rwm]... ;..."
}
```

* задаем команду
```
portoctl set container_name command 'sleep 10'
```

* запускаем контейнер
```
portoctl start container_name
```

>также все это можно сделать одной коммандой
portoctl exec или portoctl run, например:
```
portoctl run container_name root=/place/porto_volumes/1/volume net=inherited
resolv_conf='nameserver fd64::1' devices='/dev/nvidia1234 rw; /dev/nvidia567 rw'
command='sleep 10' net_limit='1K' cpu_limit='1.5c'
```

* остановить контейнер можно командой
```
portoctl stop container_name
```
при этом порто посылает процессу сначала SIGTERM, после чего, SIGKILL в течении заданного времени если процесс не завершается.

* удалить и остановить если он еще запущен можно через
```
portoctl destroy container_name
```
destroy разбирает контейнер в любом состоянии, отправляя SIGKILL процессам в нем


### Смонтировать arc в контейнере без CAP_SYS_ADMIN
[PORTO-796](https://st.yandex-team.ru/PORTO-796)

запускаем контейнер с чрутом, без cap_sys_admin
```
$ portoctl exec -L ubuntu-bash abc command=bash capabilities[SYS_ADMIN]=false
```
через unshare создаем mount namespace + user namespace с мапингом текущего пользователя в root
```
$ unshare -rm bash
$ arc mount -m arcadia/ -S store/
```


### Скопировать данные с/на хоста в контейнер

* создадим вольюм с [образом ubuntu-xenial](https://sandbox.yandex-team.ru/resource/1306122440/view)
```
$ portoctl vcreate -A layers='ubuntu-xenial'
/place/porto_volumes/1/volume
```

* запустим контейнер с чрутом
```
$ portoctl run a command='wget ya.ru' root='/place/porto_volumes/1/volume'
```

* дождемся завершения контейнера
```
$ portoctl wait a
```

* узнаем root_path контейнера
```
$ portoctl get a root_path
/place/porto_volumes/1/volume
```
> root_path - пусть к корню контейнера в неймспейсе клиента

* скопируем полученный файл на хост
```
cp /place/porto_volumes/1/volume/index.html .
```

аналогично можно копировать данные с хоста в контейнер


## Как сварить слой

### Сборка слоёв с помощью portoctl build

Слои рекомендуется паковать в zstd, т.к. это позволит существенно ускорить запаковку/распаковку за счет мультредовой compress/decompress.

Примеры скриптов отсюда: [https://arcanum.yandex-team.ru/robots/trunk/genconf/PORTOVM/EXPERIMENTAL/](https://arcanum.yandex-team.ru/robots/trunk/genconf/PORTOVM/EXPERIMENTAL/)
Новые RTC скрипты: [https://a.yandex-team.ru/robots//trunk/genconf/PORTOVM/COOKBOOK.md](https://a.yandex-team.ru/robots//trunk/genconf/PORTOVM/COOKBOOK.md)
Примеры в исходниках: [https://bb.yandex-team.ru/projects/PORTO/repos/porto/browse/layers](https://bb.yandex-team.ru/projects/PORTO/repos/porto/browse/layers)

Базовый слой готовится двумя скриптами: bootstrap обычно с debootstrap внутри и собственно скрипт обновляющий и устанавливающий базовый набор пакетов.
bootstrap скрипт работает в специальном bootstrap слое/чруте, остальные скрипты работаю уже в целевом чруте.

Следующие слои строятся одним скриптом и сохраняются как дельта относительно нижележащего стэка.

Сборка bootstrap слоя (нужен sudo)
```
$ sudo portoctl build -B bootstrap_bootstrap.sh -o bootstrap.zst net=inherited
$ portoctl layer -I bootstrap bootstrap.zst
```

Сборка базового слоя (sudo уже не нужен)
```
$ portoctl build -l bootstrap -B bootstrap_ubuntu_precise.sh -S base_ubuntu_precise.sh -S common-cleanup.sh -o ubuntu-precise-base.zst net=inherited
```
Сборка второго слоя (базовый тарбол автоматически импортируется во временный слой)
```
$ portoctl build -L ubuntu-precise-base.zst -S common-update.sh -S common-devel.sh -S common-cleanup.sh -o ubuntu-precise-devel.zst net=inherited
```
Третий слой (слои указываются в порядке от верхнего к нижнему)
```
$ portoctl build -L ubuntu-precise-devel.zst -L ubuntu-precise-base.zst -S common-update.sh -S XXX.sh -S YYY.sh -S -S common-cleanup.sh -o ubuntu-precise-XXX.zst net=inherited
```

Запуск с опцией -M склеивает все слои в один самодостаточный tarball (можно использовать вместе со скриптами или позже склеить готовые слои)
```
$ portoctl build -M -L ubuntu-precise-devel.zst -L ubuntu-precise-base.zst -o ubuntu-precise-base-devel.zst
```

Опция -O image.img собирает ext4 слой вместо tarball, требуется дополнительно указать размер
```
$ portoctl build -L ubuntu-precise-base.tgz -O ubuntu-precise-base-devel.zst space_limit=10G
```
Для сети (net=...) проще использовать inherited(сеть хоста), IPv6 SLAAC (RA) или NAT

### Сборка слоёв в sandbox

{% note alert %}

Данный способ объявлен устаревшим.

{% endnote %}

Сборка с помощью таски [BUILD_PORTO_LAYER](https://sandbox.yandex-team.ru/tasks?type=BUILD_PORTO_LAYER).

Ссылки на скрипты в аркадию: ```arcadia:/path[@rev]```
Можно ссылаться на скрипты по http, например cюда: https://paste.yandex-team.ru/XXXX/text

Скриты рекомендуется коммитить в [https://arcanum.yandex-team.ru/robots/trunk/genconf/PORTOVM/](https://arcanum.yandex-team.ru/robots/trunk/genconf/PORTOVM/):
```
svn co svn+ssh://arcadia.yandex.ru/robots/trunk/genconf/PORTOVM/
```
При сборке указывается пути вида `arcadia:/robots/trunk/genconf/PORTOVM/<script.sh>`

Ресурс: PORTO_LAYER* - tar архив слоя, PORTO_IMAGE* - ext4 слой.

Для запуска bootstrap скрипта автоматически используется последний релиз слоя `PORTO_LAYER_BOOTSTRAP`

### Сборка слоёв в arcadia

Образы собираются прямо в аркадии с помощью [ya make](https://docs.yandex-team.ru/ya-make/). Подробности доступны по [ссылке](./virtual-images.md#diy).

## Жизнь с лимитами по ресурсам

В порто есть следующие лимиты, гарантии, и метрики, по которым можно определять недостаток текущего лимита:

### CPU

* cpu_guarantee - гарантия в ядрах (1.5c) или процентах хоста (15)
* cpu_guarantee_total - итоговая гарантия для поддерева
* cpu_guarantee_total = max(cpu_guarantee, sum cpu_guarantee_total для running дочерних контейнеров).
* cpu_guarantee_bound - maximum guarantee of upper hierarhy
* cpu_limit - квота в ядрах (1.5c) или процентах хоста (15)
* cpu_limit_total - итоговое максимальное потребление для поддерева
* cpu_limit_bound - минимальный лимит родительского дерева


* cpu_wait - время ожидания исполнения процессов (ns)
* cpu_throttled - время ожидания при нехватке квоты (ns)


### Memory

* memory_guarantee - объём защищённый от реклеймера. default: 0
* memory_guarantee_total - общие гарантии по иерархии
memory_guarantee_total = max(memory_guarantee, sum memory_guarantee_total для running подконтейнеров)
* memory_limit жёсткий лимит для memory_usage
для контейнера 1 уровня по умолчанию равен max(Total - 2Gb, Total * 3/4), для остальных уровней 0 (unlimited).
Margin from total ram (2Gb) указывается в portod.conf:
```
container {
    memory_limit_margin: <bytes>
}
```
При неудачном системном вызове, вернувшем ENOMEM / EFAULT, page fault вызывает OOM.
* memory_limit_total - общий лимит по иерархии
memory_limit_total = min(memory_limit, memory_limit_total для родительского контейнера)
* anon_limit - лимит на анонимную память
по умолчанию равно memory_limit - min(memory_limit / 4, 16M).
Default margin from limit (16Mb) указывается в in portod.conf:
```
container {
    anon_limit_margin: <bytes>
}
```
* anon_limit_total - общий лимит по иерархии
anon_limit_total = min(anon_limit, anon_limit_total for parent)
* anon_only - только анонимная память, файловый кэш аллоцируется в родительской цгруппе
* dirty_limit лимит на объём незаписанного файлового кэша
* recharge_on_pgfault - перемещать файловый кэш на фолтах
* pressurize_on_death - после смерти контейнера приоритезировать реклейм её кэша
* oom_is_fatal - убивать весь контейнера в случае OOM, по умолчанию
* oom_score_adj - управление OOM -1000..1000, по умолчанию 0
смотри oom_score_adj в proc(5).
 * exit_code - 0: ```success, 1..255: error code, -64..-1: termination signal, -99: OOM```
* oom_killed - true, если контейнер получил OOM
* oom_kills - количество задач, убитых в контейнере с момента запуска (Linux 4.13 or offstream patches)
* oom_kills_total - количество задач убитых в контейнере и его подконтейнерах с момента запуска (Linux 4.13 or offstream patches)
* core_dumped - true, если процесс сделал core dump


### Network

* net_guarantee - гарантированный bandwidth: ```<interface>|group <group>|default: <Bps>;...```
>
* eth0 CS0" - исходящая гарантия для CS0 на eth0 на хосте
* CS0 - исходящая гарантия для CS0 на каждом выходном канале хоста
* eth0 - исходящая гарантия для каждого класса на eth0 интерфейсе на хосте
* default - гарантия по умолчанию для всего

* net_limit - лимит bandwidth на отправку ```<interface>|group <group>|default: <Bps>;...```
>
* "eth0 CS0" - исходящий лимит для CS0 на eth0 на хосте
* CS0 - исходящий лимит для CS0 на каждом выходном накале хоста
* veth - общий исходящий лимит для net="L3 veth"
* default - лимит по умолчанию для всего
* CS7: 1 - blackhole

* net_rx_limit - лимит bandwidth на получение ```<interface>|group <group>|default: <Bps>;...```
* net_drops - tc drops: ```<interface>|<class>: <packets>;...```
* net_overlimits - tc overlimits: ```<interface>|<class>: <packets>;...```
* net_packets - tc packets: ```<interface>|<class>: <packets>;...```
* net_rx_drops - дропы при получении: ```<interface>|group <group>: <packets>;...```
* net_tx_drops - дропы на отправке: ```<interface>|group <group>: <packets>;...```


### IO

* io_limit - лимит bandwidth ввода/вывода: ```fs|<path>|<disk> [r|w]: <bytes/s>;...```
* io_ops_limit - лимит на чисто io операций в секунду: ```fs|<path>|<disk> [r|w]: <iops>;...```

### Прочие лимиты

 * stdout_limit - периодически, когда размер превышает stdout_limit заголовочная часть удаляется с помощью fallocate(2).
Количество потерянных байт отображается в  stdout_offset.
 * thread_limit - лимит на количество тредов
 * ulimit - ограничения ресурсов, ```<type>: [soft]|unlimited <hard>|unlimited; ... getrlimit(2)```
Дефолтные ulimits могут быть заданы в конфиге portod.conf:
```
container {
    default_ulimit: "type: soft hard;..."
}
```
Не изменяемые дефолты
```
"core: 0 unlimited; nofile: 8K 1M"
```

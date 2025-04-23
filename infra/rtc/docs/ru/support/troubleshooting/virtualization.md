#  Системы виртуализации (Porto/QYP)
## PORTO {#porto}
### Отличаются показатели du и df {#df_du_diff}
**Если у вас нет доступа на хост машину для применения рецепта из 2го пункта, обратитесь в чат поддержки RTCSUPPORT**

В данном случаем проблема может иметь две причины:

1. В системе присутствуют удаленные файлы, заблокированные процессом. Диагностировать данную проблему можно следующим образом
`lsof +D ${path} | grep -i deleted | awk '{print $7}'` - выведет размеры удаленных файлов
`lsof +D ${path} | grep -i deleted | awk '{print $7}'| paste -sd+| bc -l` - выведет суммарный объем удаленных файлов в байтах
если суммарный объем сопоставим с разницей между показаниями `du` и  `df`, привести все в норму поможет перезапуск процесса, который удерживает файлы,
pid данного процесса можно узнать из вывода `lsof +D ${path}| grep deleted| awk '{print $2}'`
1. При перезагрузке хоста не очищается утилизация дисковой квоты для porto volume. Диагностировать данную проблему нужно следующим образом.
Суммарный объем удаленных файлов(см. предыдущий пункт) не сопоставим с разницей между показаниями du и  df, либо удалённых файлов вообще нет,
а в выводе команды `project_quota info ${path}` значения `usage` и `limit` равны.
В этом случае нужно будет запустить `project_quota check ${path}` . Это восстановит аккаунтинг квоты. Время работы зависит от количества файлов.

**Важно:** время работы команды lsof сильно зависит от количества процессов, размера файловой системы и нагрузки на диск, в связи с этим, работать они может долго.
В данных примерах переменная ${path} в большинстве случаев это путь к porto volume.

### Как определить путь до porto volume на хост машине {#porto_volume}
**Данная процедура подразумевает наличие доступа на хост машину**

Чтобы узнать список volume у контейнера, воспользуйтесь командой:
`portoctl vlist -c <container_name>`, полное имя контейнера можно узнать из вывода команды `portoctl list`
Пример вывода:

```
root@man2-2589:~# portoctl vlist -c ISS-AGENT--t5cgqfsvwjgkaelw/t5cgqfsvwjgkaelw_maps_core_nmaps_acl_stable_dfbd5wWbjlU/iss_hook_start
Volume                                  ID      Backend      Limit      Used     Avail Use% Containers
/                                       3879    overlay         2G     99.1M      1.9G   5% ISS-AGENT--t5cgqfsvwjgkaelw/t5cgqfsvwjgkaelw_maps_core_nmaps_acl_stable_dfbd5wWbjlU
/logs                                   2257    native        100G    543.8M     99.5G   1% ISS-AGENT--t5cgqfsvwjgkaelw/t5cgqfsvwjgkaelw_maps_core_nmaps_acl_stable_dfbd5wWbjlU(/logs)
/place/db/iss3/instances/t5cgqfsvwjgkaelw_maps_core_nmaps_acl_stable_dfbd5wWbjlU
                                        3880    native          1G      2.9M   1021.1M   0% ISS-AGENT--t5cgqfsvwjgkaelw/t5cgqfsvwjgkaelw_maps_core_nmaps_acl_stable_dfbd5wWbjlU(/place/db/iss3/instances/t5cgqfsvwjgkaelw_maps_core_nmaps_acl_stable_dfbd5wWbjlU)
```

В данном случае нам нужны столбцы Volume и ID, первый позволит вам опознать том по имени внутри контейнера, второе поле нужно для поиска на хост машине.

- Найдите по названию нужный вам volume
- Возьмите его ID
- Путь к тому может быть двух видов /place/porto_volumes\/<ID\>/volume, для томов расположенных на HDD и /ssd/porto_volumes/<ID>/volume для расположенных на SSD. По данным путям будут доступны данные
находящиеся в томе.

### Ошибка porto permission denied /dev/kvm {#porto_dev_kvm}
**решить данную проблему можно через RTCSUPPORT**

Все инстансы в RTC облаке работают от имени пользователя `loadbase` следовательно для использования /dev/kvm пользователь `loadbase`
должен быть добавлен в группу kvm и фактически при диагностике проблемы, такое условие выполняется. Но в ряде случаев запуск ISS агента может произойти раньше
чем `loadbase` будет добавлен в группу kvm, в итоге получаем ошибку `porto permission denied /dev/kvm`

{% cut "Действия для дежурного RTCSUPPORT" %}

```
portod reload
с последующим перезапуском iss_agent
restart yandex-iss-agent - для ubuntu с upstart в качестве init системы
systemctl restart yandex-iss-agent.service - для systemd
```

{% endcut %}

### Вымывание кэша бинарников в место OOM {#porto_anon_limit}
В некоторых редких случаях в контейнере может вымыться кэш бинарника вместо OOM при подходе к memory_limit, например, [SPI-17318](https://st.yandex-team.ru/SPI-17318). Чтобы от этого защититься нужно выставить anon_limit.

Планку anon_limit должен выставлять владелец приложения, тк для этого необходимо быть знакомым с анатомией сервиса и точно понимать и постоянно следить за его штатным средним уровнем потребления анонимной памяти (и приемлемыми флуктуациями) - автоматически его выставлять на этапе аллокации пода мы точно не хотим, т.к. с точки зрения платформы это будет происходит "наугад".

Массового опыта использования anon anon_limit у нас в платформе также нет, а возможность выставить - есть.
Краткая инструкция - ставить с запасом относительно прогнозируемого уровня потребления анонимной памяти или с некоторым зазором относительно, чуть меньше (типично - на 100-200М) лимита по памяти всего контейнера.
Требуемый зазор можно также примерно высчитывать как суммарный размер working set-а самих запускаемых бинарей, их библиотек (при наличии) и входных файлов, которые должны находиться в памяти.

## QYP {#qyp}
### FAQ & Wiki {#where_is_the_faq}
Часть FAQ живёт всё ещё в [wiki](https://wiki.yandex-team.ru/qyp/faq/).

### ВМ перешла в состояние Porto socket error:INVALID {#qyp_porto_socket_error}
**Данную проблему можно решить только с участием RTCSUPPORT**
При выполнении команды

```
vmctl status --cluster <SAS|MAN|VLA> --pod-id <vm_name>
```
или в UI QYP вы видите состояние

```
"state": {
"info": "Porto socket error",
"type": "INVALID"
},
```
и vm не реагирует на start, ва мнеобходимо обратиться в чат поддержки RTCSUPPORT, у казанием ссылки на вашу VM в UI QYP или создать тикет в очередь RTCSUPPORT с
заголовком **Porto socket error <vm_name>**, после чего дежурный RTCSUPPORT реанимирует вашу ВМ.
После того, как действия дежурного выполнены, вам необходимо проверить версию vm-agent, если версия меньше 0.18, агент следует обновить. Для этого
Выключите vm `vmctl poweroff --cluster <SAS|MAN|VLA> --pod-id <vm_name>` или через UI QYP
обновите vm-agent до последней версии
включите машину `vmctl start --cluster <SAS|MAN|VLA> --pod-id <vm_name>` или через UI QYP

{% cut "Действия дежурного RTCSUPPORT" %}

После чего не реагирует на start.
Причина: при перезагрузке хоста перестает отвечать porto и ВМ застревает в этом состоянии. Поведение было поправлено в vmagent начиная с версии 0.14.
Для избежания повторения ошибки рекомендуется после починки обновить vmagent через vmctl/QYP UI или Nanny (для gencfg).
**Как чинить:**

1. Зайти в /iss_hook_start контейнер ВМ (пример: `ISS-AGENT--my-shiny-vm/my-shuny-vm_qyp_M3zAcEGy3uH/iss_hook_start`)
1. `rm /qemu-persistent/last_status`
1. `curl -d "" -H "Local-Token: `cat /tmp/vmagent.token`" -g 'http://[::1]:7255/debug?cmd=shutdown'`
1. Дождаться ответа от vmctl, ВМ будет в состоянии STOPPED. Запустить ее
1. Из-за внезапного рестарта могла побиться фс. В таком случае выполнить fsck из rescue shell
UDP: Если ВМ аллоцирована через gencfg то в пункте 3 замените ссылку на следующую `'http://[::1]:<BSCONFIG_IPORT>/debug?cmd=shutdown'`, значение BSCONFIG_IPORT можно узнать из файла dump.json внутри контейнера командой:
`grep BSCONFIG_IPORT dump.json` или используйте порт на котором слушает vmagent узнать этот порт можно командой

```netstat
tcp6 0 0 :::32340 :::* LISTEN 52826/vmagent
netstat -anpl | grep vmagent | awk '{print $4}' | grep -oE '[0-9]*' <- для получения просто номера порта.
```

{% endcut %}

### Взаимодействие персональных и групповых квот в QYP {#qyp_personal_quotas}
Групповая квота делится на количество человек в группе и вычитается из персональной:
**При подсчете учитываются все локации групповой квоты.**
Размер вычитаемых ресурсов групповой квоты из персональной вычисляется так:
    Берется CPU/MEM/DISK(без разделения на HDD & SSD)/IP
    Делится на количество человек в сервисе, не считая роботов
    Округляется в большую сторону.

[wiki](https://wiki.yandex-team.ru/qyp/personal_quota/#1vozmozhnoliispolzovaniekakgruppovyxtakipersonalnyxkvot)
[RTCSUPPORT-3773](https://st.yandex-team.ru/RTCSUPPORT-3773#5cf1240f3932cc001f0fc8f8)

### Не резолвится DNS-имя ВМ QYP при подключении через VPN {#qyp_resolve}
В случае, если при попытке подключения к ВМ под VPN, возникает ошибка вида:
```
ssh: Could not resolve hostname <VM name>: Name or service not known

```
Необходимо проверить настройки подключения из инструкции по настройке VPN: https://wiki.yandex-team.ru/diy/linux/vpn/
В частности, проверить наличие дополнительных DNS-серверов
```
Для IPv4 указываем дополнительный DNS 213.180.205.1
Для IPv6 указываем дополнительный DNS 2a02:6b8::1:1

```

### ВМ не грузится с ошибкой в VNC "No bootable device" {#qyp_no_bootable_device_qcow2}
**Данную проблему можно решить только с участием RTCSUPPORT**
Сейчас наблюдается редкая ошибка с QYP VM, имеющие тип диска(image type) qcow2, которая выражается в циклическом ребуте VM из-за отсутствия загрузочного диска.
Если у вашей VM в VNC наблюдается ошибка "No bootable device", необходимо завести тикет в очереди RTCSUPPORT с описанием проблемы и ссылкой на VM из QYP.

{% cut "Действия дежурного RTCSUPPORT" %}

**Диагностика**
1. Проверить, что VM имеет тип диска qcow2
2. Зайти в контейнер iss_hook_start
3. Выполнить `qemu-img info /qemu-persistent/current.qcow2`
Результат должен быть примерно такой

```
## qemu-img info /qemu-persistent/current.qcow2
image: /qemu-persistent/current.qcow2
file format: qcow2
virtual size: 0 (0 bytes)
disk size: 192K
cluster_size: 65536
Format specific information:
compat: 1.1
lazy refcounts: false
refcount bits: 16
corrupt: false

```

В поле virtual size 0 байт – это оно.

**Как чинить**
1. Остановить ВМ (poweroff)
2. Удалить /qemu-persistent/current.qcow2
3. Запустить ВМ

Разбор проблемы ведётся в тикете [QEMUKVM-672](https://st.yandex-team.ru/QEMUKVM-672).
Стоит линковать все тикеты с проблемными VM к нему.

{% endcut %}

### Контейнер ВМ в состоянии HOOK_SEMI_FAILED {#qyp_hook_semi_failed}
Состояние HOOK_SEMI_FAILED в контейнере в ВМ означет, что vmagent внутри контенера не отвечает на ручку ping,
проверить данную проблему можно командой(выполнять внутри контейнера)
```
curl https:$(uname -n):7255/ping

```
Причины данной проблемы могут быть разными, ниже проявления с которыми сталкивались:

{% cut "Большой образ ВМ" %}

[RTCSUPPORT-5008](https://st.yandex-team.ru/RTCSUPPORT-4164)
Продиагностировать можно следующим образом:
- Смотрим лог vmagent, который надиться внутри контейнера с ВМ по пути /quemu-persistent/logs/vmagent.log
```
cat /qemu-persistent/logs/vmagent.log
kigan-img 70 2019-07-24 17:52:36,411 INFO  [VMWorker] Start initial configuration process
kigan-img 70 2019-07-24 17:52:36,411 INFO  [VMWorker] Applying config
id: "empty"
vcpu: 32
mem: 42949672960
disk {
resource {
rb_torrent: "rbtorrent:ef9f53e986edc46b86731327faf9561d7bc81087" <--- rbtorrent ссылка на образ
}
path: "/"
type: RAW
}
access_info {
vnc_password: "396d4a7c"
}
autorun: true
kigan-img 70 2019-07-24 17:52:36,411 INFO  [VMWorker] Set new state: type: BUSY
generation: 2

kigan-img 70 2019-07-24 17:52:36,987 INFO  [VMWorker] Set new state: type: PREPARING

```
проверить размер образа можно командой
```
sky files <rbtorrent_url>

```
сравнить с файлом который скачивается в данный момент
```
ls -lh /qemu-persistent/image_folder
-rw-rw-r-- 1 loadbase loadbase 247G Jul 25 13:25 layer.img

```
Если признаки совпадают остается дождаться пока образ будет полностью скачен.

{% endcut %}

### Не работает sky get внутри QYP VM {#qypskytimeout}
Симптомы:
При скачивании ресурса через sky get или иным способом, получаем ошибку
```
Error: ResourceDownloadError: Unable to receive resource info in 60 seconds
```

После эвакуации ВМ с железного хоста может сохраниться некорректная настройка Fastbone-интерфейса, что приведёт к невозможности закачки ресурсов с помощью утилиты sky.
Выражается в недоступности FQDN `fb-<VM name>.<DC name>.yandex.net` по пингу:
```
ping6 fb-rtcbutler-dev.sas.yp-c.yandex.net
PING fb-rtcbutler-dev.sas.yp-c.yandex.net(fb-rtcbutler-dev.sas.yp-c.yandex.net) 56 data bytes
^C
--- fb-rtcbutler-dev.sas.yp-c.yandex.net ping statistics ---
33 packets transmitted, 0 received, 100% packet loss, time 32256ms

```

Исправить можно очистив информацию об интерфейсах внутри ВМ и перезагрузив её, для получения актуальных данных:

Изнутри ВМ запустить команду из под root:

{% list tabs %}

- Ubuntu >= 16.04

  `cloud-init clean`

- Ubuntu < 16.04

  `rm -rf /var/lib/cloud/instances`

{% endlist %}

Затем перезагрузить ВМ.

После этого FQDN FB-интерфейса должен стать доступен и снова появится возможность скачивать ресурсы через sky get

### VM периодически зависает, при этом в коносли информация о баге в timer.c {#qyp_timer_bug}
**Симптомы**
ВМ периодически зависает в случайное время, при этом в консоли(VNC) выводится стек-трейс вида
```
[4228131.350579] ------------[ cut here ]------------
[4228131.351442] CPU: 1 PID: 0 Comm: swapper/1 Not tainted 4.19.55-9 #1
[4228131.352130] kernel BUG at kernel/time/timer.c:1154!
[4228131.352986] Hardware name: QEMU Standard PC (i440FX + PIIX, 1996), BIOS rel-1.10.2-0-g5f4c7b1-prebuilt.qemu-project.org 04/01/2014
[4228131.355205] RIP: 0010:run_timer_softirq+0x13c/0x460

```

**Как чинить**
Баг известный [KERNEL-283](https://st.yandex-team.ru/KERNEL-283). Workaround - перезагрузка ВМ. Полное исправление - обновить ядро в VM. Актуальную версию можно взять с [wiki](https://wiki.yandex-team.ru/kernel/#branch4.19).

{% cut "Инструкция по обновлению ядра до 4.19.100-23" %}

Все последующие действия внутри ВМ производятся из под root'а (У Owner'ов ВМ есть возможность логиниться из под пользователя root).
 - Проверяем открыт ли фаервол до dist.yandex.ru. Если правил нет - их необходимо заказать.
Вместо \_SEARCHSAND\_ необходимо подставить сетевой макрос вашей VM.
https://puncher.yandex-team.ru/?source=\_SEARCHSAND\_&destination=dist.yandex.ru&rules=exclude_rejected&values=all&sort=destination
 - Проверяем наличие дистрибутивов и ключей, [wiki](https://wiki.yandex-team.ru/kernel/#install)
Нас интересуют stable & unstable ветки:
```
## cat /etc/apt/sources.list.d/yandex-search-kernel.list
## These are Yandex.Search repositories for Linux kernel
deb [http://search-kernel.dist.yandex.ru/search-kernel](http://search-kernel.dist.yandex.ru/search-kernel) stable/all/
deb [http://search-kernel.dist.yandex.ru/search-kernel](http://search-kernel.dist.yandex.ru/search-kernel) unstable/all/

deb [http://search-kernel.dist.yandex.ru/search-kernel](http://search-kernel.dist.yandex.ru/search-kernel) stable/amd64/
deb [http://search-kernel.dist.yandex.ru/search-kernel](http://search-kernel.dist.yandex.ru/search-kernel) unstable/amd64/

```
Ключи можно посмотреть следующей командой:
```
apt-key list
...
pub   4096R/43E69418 2016-05-27
uid                  Yandex Public Repository Sign Key [opensource@yandex-team.ru](opensource@yandex-team.ru)
sub   4096R/5EFF1579 2016-05-27

pub   1024D/6050CD1A 2010-01-18
uid                  Yandex Public Repository Sign Key [opensource@yandex-team.ru](opensource@yandex-team.ru)
sub   4096g/34059849 2010-01-18

```
Добавляем их по инструкции по ссылке, если репозиториев, или ключей нет.
Для получения ключа по инструкции из ссылки(если он отсутствует) нужен будет доступ в интернет через NAT64. Дозаказываем доступы в Puncher и включаем NAT64 в ВМ.
- Обновляем информацию о пакетах в дистрибутиве: `apt-get update`
- Устанавливаем последнее стабильное ядро: `apt-get install linux-image-server`
- Устанавливаем версию ядра с фиксом. Его необходимо устанавливать отдельно, т.к. на данный момент оно помечено как unstable:
```
## apt-get install linux-image-4.19.100-23
## apt-get install linux-image-extra-4.19.100-23
## apt-get install linux-headers-4.19.100-23
```
 - Перезагружаем ВМ: %%# reboot%%
 - Проверяем, что запустилось новое ядро:
```
## uname -r
4.19.100-23

```

{% endcut %}

### Проверка передачи GPU виртуальной машине. {#gpu_check}
#### GPU в QYP
GPU в виртуальные машины закидываются без использования драйверов nvidia. Через механизм vfio, т.е. как PCI устройство. Соответственно драйвера nvidia на ноду не устанвливаются.
Чтобы "закинуть" GPU в контейнер/виртуалку, iss-agent обращается к nvgpu-manager'у на хосте. Тот должен вернуть ответ с координатами того, что и как надо закинуть в контейнер.

#### Диагностика
Диагностировать можно так:
В iss-agent.log ищем Exception:
```
2020-08-26 10:28:36.211 [system-akka.actor.default-dispatcher-3] INFO  - Pod iva with instances not synchronized:
|ru.yandex.iss.agent.exceptions.FailureStateException
|  @ OUTSIDE_OF_DRIVER
|  : GPU_ALLOCATION_FAILED
...
GpuDevicesRequest{mode=vfio, devices=[00d14d6e-c715-557f-b2b8-7ca0ca852229...

```
Т.е. сделали запрос на аллокацию устройств в контейнер (режим и список uuid), на что получили ответ:
```
NOT_FOUND: Device not found, id: 00d14d6e-c715-557f-b2b8-7ca0ca852229

```
Т.е. сервер (YP) выделил на запрос пода конкретные устройства, а их нет. Проверить можно с помощью `sudo nvgpuctl list`.

```
iva1-5739:~$ sudo nvgpuctl list
+--------+----+-------+--------+------+--------+------+-------+-----------+------+------+------+
| BUS ID | ID | MODEL | MEMORY | NUMA | DRIVER | CUDA | READY | THROTTLED | TEMP | USED | FREE |
+--------+----+-------+--------+------+--------+------+-------+-----------+------+------+------+
+--------+----+-------+--------+------+--------+------+-------+-----------+------+------+------+
+--------------+--------------------------------------+----------------+--------+------+-------------+
|    BUS ID    |                  ID                  |     MODEL      | MEMORY | NUMA | IOMMU GROUP |
+--------------+--------------------------------------+----------------+--------+------+-------------+
| 0000:04:00.0 | 95a6abdd-c360-5294-a21e-304cd005aaa5 | gpu_tesla_v100 |  16384 |    0 |          45 |
| 0000:05:00.0 | 4149962a-4e77-5aa6-9c18-66c199a732c3 | gpu_tesla_v100 |  16384 |    0 |          46 |
| 0000:08:00.0 | 8a724a2a-8b50-5d4b-a15a-7ada5f38fc98 | gpu_tesla_v100 |  16384 |    0 |          50 |
| 0000:09:00.0 | 80f5da19-8713-560f-b21c-9fbcf0311875 | gpu_tesla_v100 |  16384 |    0 |          51 |
| 0000:84:00.0 | c63388d4-6bde-5a32-b0ea-1fb211a7b292 | gpu_tesla_v100 |  16384 |    1 |          63 |
| 0000:85:00.0 | f0342faf-3032-5ccb-be01-dd746c1e986d | gpu_tesla_v100 |  16384 |    1 |          64 |
| 0000:88:00.0 | 0c2ef8f0-2150-52c0-8a4d-00ea3ee5869f | gpu_tesla_v100 |  16384 |    1 |          68 |
| 0000:89:00.0 | a6d15921-0d56-5e55-929c-ce827e356d63 | gpu_tesla_v100 |  16384 |    1 |          69 |
+--------------+--------------------------------------+----------------+--------+------+-------------+

```
Дальше проверяем наличие нужных UUID и выясняем, почему нужный UUID отсутствует в List.
Обычно UUID устройств меняются при переналивке хоста, и данные по какой-то причине не доехали в планировщик(YP).
Маршрутизация проблемы зависит от причины, по которой данные в планировщике не обновились: [RTCSUPPORT-7251](https://st.yandex-team.ru/RTCSUPPORT-7251#5f461c0e558e052f3a2ecfd7)

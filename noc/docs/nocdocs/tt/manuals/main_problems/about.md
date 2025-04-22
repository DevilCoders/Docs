# Описание типовых проблем и методы их решения

Автор: [ezhichek@]((https://staff.yandex-team.ru/ezhichek))

## Принудительное снятие анонса с балансера
Предположим, что необходимо потушить анонс какого-то сервиса на балансере,
для примера возьмем yastat.net и потушить нужно анонс адреса 77.88.44.144 с балансера myt-lb6b:
![](_images/img.png)

Заходим на балансер myt-lb6b и ищем в конфиге keepalived.conf инструкцию для снятия анонса сервиса:
```(sh)
$ egrep -r 77.88.44.144 /etc/keepalived | grep -v autoconfig | grep down
/etc/keepalived/keepalived.conf:        quorum_down "/etc/keepalived/quorum-handler2.sh down 77.88.44.144,b-100,2"
/etc/keepalived/keepalived.conf:        quorum_down "/etc/keepalived/quorum-handler2.sh down 77.88.44.144,b-100,2"
```
Здесь мы видим, что при достижении нижнего порога вызывается
```/etc/keepalived/quorum-handler2.sh down 77.88.44.144,b-100,2```.
Записи две, потому что у сервиса есть 80 и 443 порты, каждый из которых влияет на анонс.

Чтобы снять анонс VIP с балансера выполняем приведенную выше команду и смотрим RT:
```(sh)
# /etc/keepalived/quorum-handler2.sh down 77.88.44.144,b-100,2
```
![](_images/img_1.png)

Чтобы поднять анонс — заменяем down на up:
```(sh)
# /etc/keepalived/quorum-handler2.sh up 77.88.44.144,b-100,2
```
### Снятие анонса сервиса с балансера в регионе
Сервисы в регионах живут каждый в своей сети. Так необходимо для правильной работы anycast адресов.
Поэтому при снятии анонса сервиса в регионе **обязательно** необходимо убрать **все** адреса этого сервиса.

## Замена диска в балансере
### Удаление диска и создание тикета
- просмотр состояния рейда:
```(sh)
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
md0 : active raid1 sdb2[1](F) sda2[0]
      9757568 blocks super 1.2 [2/1] [U_]
md1 : active raid1 sdb3[1] sda3[0]
      5849633600 blocks super 1.2 [2/2] [UU]
```
Здесь видно, что проблема с sdb2 в рейде md0.
Если диск в состоянии failed, то стоит его сначала отстрелить
из обоих рейдов в данном случае:
```(sh)
# mdadm /dev/md0 -r /dev/sdb2
mdadm: hot removed /dev/sdb2 from /dev/md0

# mdadm /dev/md1 -f /dev/sdb3
mdadm: set /dev/sdb3 faulty in /dev/md1
# mdadm /dev/md1 -r /dev/sdb3
mdadm: hot removed /dev/sdb3 from /dev/md1
```

Тут видно, что если диск из одного из рейдов не отстрелился,
как в случае с sdb и md1, то его нужно сначала пометить как
failed, а потом отстрелить.

Узнаем серийный номер диска:
```(sh)
# smartctl -i /dev/sdb | grep -i serial
Serial Number:    76MAK89HFTMB
```
Если smartctl команды нет, то нужно поставить smartmontools:
```(sh)# apt-get install smartmontools```
Если наш диск отвалился так, что нельзя определить его серийный номер,
то можно методом исключения посмотреть в [golem-е](https://golem.yandex-team.ru) список дисков, и методом исключения найти проблемный, например:
[https://golem.yandex-team.ru/hostinfo.sbml?object#vla1-2lb1b.yndx.net](https://golem.yandex-team.ru/hostinfo.sbml?object=vla1-2lb1b.yndx.net)

![](_images/img_2.png)

Поиск номера диска для замены:
```(sh)
# ls -la /sys/block/|grep sd
lrwxrwxrwx  1 root root 0 дек.  25 15:33 sda -> ../devices/pci0000:00/0000:00:11.4/ata1/host0/target0:0:0/0:0:0:0/block/sda
lrwxrwxrwx  1 root root 0 дек.  25 15:33 sdb -> ../devices/pci0000:00/0000:00:11.4/ata2/host1/target1:0:0/1:0:0:0/block/sdb
```

Здесь ссылка ```targetX:0:0/X:0:0:0```, X — порядковый номер диска для замены, считается с нуля;
обычно sda — нулевой, а sdb — первый с нуля.

Теперь у нас есть всё необходимое для заявки, идём в bot и просим заменить проблемный диск:
https://bot.yandex-team.ru/adm/ — ищем балансер по серийному номеру или FQDN

{% note info %}

ставим галочку у найденного хоста > change failed HDD > Заменить неисправный диск > пишем порядковый и серийный номера > Создать

![](_images/img_3.png)

{% endnote %}

### Добавление диска
После добавления диска стоит проверить, что он появился в списке устройств:
```(sh)
# ls -la /dev/sdb*
brw-rw---- 1 root disk 8, 16 сент. 28 19:04 /dev/sdb
brw-rw---- 1 root disk 8, 17 сент. 28 19:04 /dev/sdb1
brw-rw---- 1 root disk 8, 18 сент. 28 19:04 /dev/sdb2
brw-rw---- 1 root disk 8, 19 сент. 28 19:04 /dev/sdb3
```

Если диска нет, то стоит пересканировать устройства:
```(sh)# ls /sys/class/scsi_host/|while read host_num ; do echo '- - -' >/sys/class/scsi_host/${host_num}/scan ; done```

Также надо проверить, что не запустились новые рейды с нового диска:
- аналогично смотрим /proc/mdstat и если там появились md-что-то с новым
- диском, то останавливаем из с помощью ```(sh)mdadm -S /dev/md-что-то```.
- Также при обнаружении лишних md стоит почистить суперблоки:
  - ```(sh)# ls /dev/sdb* | while read block ; do mdadm --zero-superblock ${block} ; done```

Теперь копируем GPT-таблицу разделов и добавляем диск:

```(sh)
# sgdisk -R /dev/sdb /dev/sda
The operation has completed successfully.

# mdadm /dev/md0 -a /dev/sdb2
mdadm: added /dev/sdb2
# mdadm /dev/md1 -a /dev/sdb3
mdadm: added /dev/sdb3
```

Тут обращаю внимание что каманду sgdisk следует читать как:

`sgdisk -R <куда копировать таблицу разделов — новый диск> <откуда читать таблицу разделов — старый диск>`

После того как диск засинхронизируется, нужно будет добавить загрузочную запись:

```(sh)
# grub-install /dev/sdb
```

Здесь мы везде говорили про замену /dev/sdb, всё это характерно для замены любого диска — набор действий одинаков.

## События мониторинга
### High IO
Иногда в мониторинге для балансера может появиться событие «High IO»

![](_images/img_4.png)

В этом случае в первую очередь стоит проверить что есть в dmesg:

```(sh)
# dmesg
```

и проверить состояние raid:

```(sh)
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
md1 : active raid10 sdd3[3] sdb3[1] sdc3[2] sda3[0]
      3885249536 blocks super 1.2 512K chunks 2 near-copies [4/4] [UUUU]
      [##>..................]  resync # 10.9% (425234688/3885249536) finish#710.5min speed#81152K/sec
```

В нашем случае видно, что причиной срабатывания данного алерта стал sync raid-а, почему он произошел:
- возможно кто-то заменил диск, для этого стоит посмотреть историю логинов и спросить у коллег:

```(sh)
$ last|head
ezhichek pts/0        noc-myt.yandex.n Thu Feb  1 11:57   still logged in
ya-lilo  pts/1        noc-myt.yandex.n Thu Feb  1 11:40   still logged in
ezhichek pts/0        mnt-myt.yandex.n Thu Feb  1 11:39 - 11:49  (00:10)
reboot   system boot  4.4.50-noc       Thu Feb  1 10:27 - 11:59  (01:31)
```

- или кто-то перезагрузил сервер

```(sh)
$ uptime
 11:59:59 up  1:32,  2 users,  load average: 1,26, 1,21, 1,23
```

Тут видно, что полтора часа сервер был перезагружен, что и стало причиной resync-а.

--------
[Первоисточник статьи](https://wiki.yandex-team.ru/traffic/duty-patterns/)

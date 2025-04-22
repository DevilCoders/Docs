При замене диска, особенно в случаях замены HDD на SSD, полезно переводить zfs пул на размер кластера 4kb. Это позволяет избегать вот таких неприятных ситуаций:
```
>zpool status
  pool: zroot
 state: ONLINE
status: One or more devices is currently being resilvered.  The pool will
        continue to function, possibly in a degraded state.
action: Wait for the resilver to complete.
  scan: resilver in progress since Tue May 15 10:53:08 2018
        89.5M scanned out of 12.0G at 17.9M/s, 0h11m to go
        89.3M resilvered, 0.73% done
config:

        NAME                                  STATE     READ WRITE CKSUM
        zroot                                 ONLINE       0     0     0
          mirror-0                            ONLINE       0     0     0
            diskid/DISK-BTWL318000ED480QGNp3  ONLINE       0     0     0
            diskid/DISK-PHWA645102SH240AGNp3  ONLINE       0     0     0  block size: 512B configured, 4096B native  (resilvering)

errors: No known data errors
```
Эта запись (block size: 512B configured, 4096B native) говорит о том, что диск будет изнашиваться гораздо быстрее, т.к. для перезаписи 512 байт блока носитель (SSD) перезапишет не 512 байт, а 4 килобайта.
# 1. Проверка текущего ashift

```
~>sudo zdb -C
zroot:
    version: 5000
    name: 'zroot'
    state: 0
    txg: 44677207
    pool_guid: 10363492224761479868
    hostid: 2089807972
    hostname: 'muksun.yndx.net'
    com.delphix:has_per_vdev_zaps
    vdev_children: 1
    vdev_tree:
        type: 'root'
        id: 0
        guid: 10363492224761479868
        create_txg: 4
        children[0]:
            type: 'mirror'
            id: 0
            guid: 12341491156381059427
            whole_disk: 0
            metaslab_array: 34
            metaslab_shift: 29
            ashift: 9
            asize: 96632045568
            is_log: 0
            create_txg: 4
            com.delphix:vdev_zap_top: 396
            children[0]:
                type: 'disk'
                id: 0
                guid: 5911140602658738479
                path: '/dev/gpt/root2'
                phys_path: '/dev/gpt/root2'
                whole_disk: 1
                DTL: 41
                create_txg: 4
                com.delphix:vdev_zap_leaf: 399
            children[1]:
                type: 'disk'
                id: 1
                guid: 6026056264233644456
                path: '/dev/gpt/root3'
                phys_path: '/dev/gpt/root3'
                whole_disk: 1
                DTL: 43
                create_txg: 4
                com.delphix:vdev_zap_leaf: 400
    features_for_read:
        com.delphix:hole_birth
```
Нас интересует строчка `ashift: 9` в zroot/vdev_tree/children
0
, которая говорит о том, что размер блока в данном пуле равен 512 байтам (2^9).

Это значит, что подтыкать новый диск в такой пул не стоит без конвертации. Тут далее предполагаем, что 
ada2
 - это новый диск, без разметки, который нам вставили вместо сломанного (или во имя замены на SSD). Новых дисков может быть два (
ada2
 + 
ada3
), но работать в данной инструкции мы будем только с одним, а второй можно будет подключить уже после конвертации по стандартной инструкции замены диска.
# 2. Конвертация через создание нового пула, подготовительный этап

## 2.1 Новый пул

```
# Форсим размер блока 4k 
>sysctl vfs.zfs.min_auto_ashift=12
  vfs.zfs.min_auto_ashift: 9 -> 12

# Проходимся TRIM'ом, размечаем новый диск (i поправить по месту)
export i=2; export disk=ada2
newfs -E -t -b 64k -f 64k -i 64M /dev/${disk}
gpart create -s GPT ${disk}
gpart add -s 512k -t freebsd-boot -a 4k -l boot${i} ${disk}
gpart add -s 40g -t freebsd-swap -a 4k -l swap${i} ${disk}
gpart add -s 90g -t freebsd-zfs -a 4k -l root${i} ${disk}
gpart bootcode -b /boot/pmbr -p /boot/gptzfsboot -i 1 ${disk}

# Создаем новый пул
zpool create -R /mnt z ${disk}p3
```
## 2.2 Старые снапшоты

У пула, как правило, есть снапшоты (оставшиеся, к примеру, от апгрейда машины). Если они занимают немного места (суммарно в zroot свободно более половины места), то их можно оставить. Иначе - нужно удалить часть (или все) снапшоты, чтобы свободным стало половина пространства.
```
# Показывать снапшоты
>zpool set listsnaps=on zroot
>zpool set listsnaps=on z
```
# Вот тут удалять ничего не нужно - свободно 74Gb:

{% cut "кусь" %}

```
>zfs list
NAME                                   USED  AVAIL  REFER  MOUNTPOINT
z                                      276K  86.7G    96K  /mnt
zroot                                 12.0G  74.7G  1.34G  legacy
zroot@2017-07-26                       454M      -   456M  -
zroot/usr                             3.11G  74.7G  1.57G  /usr
zroot/usr@2017-07-26                  1.55G      -  1.77G  -
zroot/usr/ports                         95K  74.7G    33K  /usr/ports
zroot/usr/ports@2017-07-26                0      -    33K  -
zroot/usr/ports/distfiles               31K  74.7G    31K  /usr/ports/distfiles
zroot/usr/ports/distfiles@2017-07-26      0      -    31K  -
zroot/usr/ports/packages                31K  74.7G    31K  /usr/ports/packages
zroot/usr/ports/packages@2017-07-26       0      -    31K  -
zroot/usr/src                           31K  74.7G    31K  /usr/src
zroot/usr/src@2017-07-26                  0      -    31K  -
zroot/var                             7.02G  74.7G  1.49G  /var
zroot/var@2017-07-26                  17.8M      -   254M  -
zroot/var/crash                         45K  74.7G  24.5K  /var/crash
zroot/var/crash@2017-07-26            20.5K      -  31.5K  -
zroot/var/db                          1.51G  74.7G  72.7M  /var/db
zroot/var/db@2017-07-26               1.42G      -  1.42G  -
zroot/var/db/pkg                      17.7M  74.7G  9.47M  /var/db/pkg
zroot/var/db/pkg@2017-07-26           8.25M      -  8.26M  -
zroot/var/empty                         42K  74.7G    24K  /var/empty
zroot/var/empty@2017-07-26              18K      -    31K  -
zroot/var/log                         1.83G  74.7G  1.67G  /var/log
zroot/var/log@2017-07-26               161M      -   259M  -
zroot/var/mail                         126M  74.7G   126M  /var/mail
zroot/var/mail@2017-07-26             47.5K      -   122M  -
zroot/var/run                          151K  74.7G  86.5K  /var/run
zroot/var/run@2017-07-26              64.5K      -  79.5K  -
zroot/var/spool                       2.06G  74.7G  49.4M  /var/spool
zroot/var/spool@2017-07-26            2.01G      -  2.01G  -
zroot/var/tmp                         1.31M  74.7G  1.28M  /var/tmp
zroot/var/tmp@2017-07-26                24K      -    40K  -
```

{% endcut %}

А вот тут нужно удалить 
zroot/var/spool@2018-09-21
, он на диске занимает 53.8Gb:

{% cut "кусь" %}

```
~>zfs list
NAME                                   USED  AVAIL  REFER  MOUNTPOINT
z                                      126M  86.6G    88K  legacy
zroot                                 71.5G  15.2G   240M  legacy
zroot@2018-09-21                      1.29G      -  1.34G  -
zroot/usr                             4.80G  15.2G  3.31G  /usr
zroot/usr@2018-09-21                  1.49G      -  1.76G  -
zroot/usr/ports                         95K  15.2G    33K  /usr/ports
zroot/usr/ports@2018-09-21                0      -    33K  -
zroot/usr/ports/distfiles               31K  15.2G    31K  /usr/ports/distfiles
zroot/usr/ports/distfiles@2018-09-21      0      -    31K  -
zroot/usr/ports/packages                31K  15.2G    31K  /usr/ports/packages
zroot/usr/ports/packages@2018-09-21       0      -    31K  -
zroot/usr/src                           31K  15.2G    31K  /usr/src
zroot/usr/src@2018-09-21                  0      -    31K  -
zroot/var                             65.1G  15.2G  3.23G  /var
zroot/var@2018-09-21                  14.7M      -  1.72G  -
zroot/var/crash                         38K  15.2G  24.5K  /var/crash
zroot/var/crash@2018-09-21            13.5K      -  24.5K  -
zroot/var/db                           161M  15.2G   108M  /var/db
zroot/var/db@2018-09-21               29.8M      -  96.6M  -
zroot/var/db/pkg                      20.9M  15.2G  10.7M  /var/db/pkg
zroot/var/db/pkg@2018-09-21           10.2M      -  10.2M  -
zroot/var/empty                         33K  15.2G    24K  /var/empty
zroot/var/empty@2018-09-21               9K      -    24K  -
zroot/var/log                         4.51G  15.2G  2.21G  /var/log
zroot/var/log@2018-09-21              2.30G      -  2.68G  -
zroot/var/mail                        37.1M  15.2G  37.0M  /var/mail
zroot/var/mail@2018-09-21             49.5K      -  35.3M  -
zroot/var/run                          159K  15.2G  84.5K  /var/run
zroot/var/run@2018-09-21              59.5K      -  76.5K  -
zroot/var/spool                       57.2G  15.2G  3.41G  /var/spool
zroot/var/spool@2018-09-21            53.8G      -  53.8G  -
zroot/var/tmp                         2.32M  15.2G  1.28M  /var/tmp
zroot/var/tmp@2018-09-21              1.03M      -  1.05M  -
```

{% endcut %}

## 2.3 Новый снапшот и первичный перенос данных

Делаем новый снапшот (использовать именно это имя снапшота!) и копируем данные:
```
zfs snapshot -r zroot@zfs4k-1
zfs send -R zroot@zfs4k-1 | zfs receive -dF z
```
## 2.4 Обновление загрузчиков

Записываем свежий загрузчик на диски, нужно выполнить для всех дисков в системе:
```
gpart bootcode -b /boot/pmbr -p /boot/gptzfsboot -i 1 ada0
bootcode written to ada0
```
Если этого не сделать, система может не загрузиться из-за того, что gptzfsboot не распознает более нового по формату пула 
z
.Если на текущих (старых) дисках в boot партиции под загрузчик отведено 64Kb, то записать свежий загрузчик не выйдет, не хватит места:`gpart: /dev/ada1p1: not enough space`В таком случае нужно открыть iKVM перед перезагрузкой и при помощи F11 загрузить сервер с SSD, где загрузчик точно обновленный.
# 3. Перезагрузка и перенос остатков данных. Восстановление зеркала

Остальная часть процесса должна происходить с отмонтированными пулами, поэтому нужна перезагрузка и использование диска в памяти в качестве корневой файловой системы. Эта часть автоматизирована в виде скрипта.
```
cd /usr/local/router/scripts
make update
sh zfs4k-convert.sh
```
Скрипт сформирует образ корневой ФС и переключит загрузку на него. Машину нужно ребутнуть и пронаблюдать за процессом. Скрипт остановится непосредственно перед перезагрузкой. Отправив машину в ребут (нажав энтер), нужно зайти в BIOS и выставить загрузку с нового SSD в первую очередь.

После успешной загрузки нужно при помощи 
dd
 стереть старые HDD, подцепить второй SSD в пул в зеркало и снести промежуточные снапшоты:
```
zfs destroy -r zroot@zfs4k-1
zfs destroy -r zroot@zfs4k-2
```
Перед затиркой нужно удалить разметку с диска `gpart destroy -F ada0`. Если диск ругается, что устройство занято, нужно проверить своп: `swapinfo`. Если в свопе только старые диски, нужно добавить новые и удалить старые:

{% cut "cut" %}

```
# swapinfo
Device          1K-blocks     Used    Avail Capacity
/dev/gpt/swap0   41943040        0 41943040     0%
/dev/gpt/swap1   41943040        0 41943040     0%
Total            83886080        0 83886080     0%
# swapon /dev/gpt/swap2
# swapon /dev/gpt/swap3
# swapoff /dev/gpt/swap0
# swapoff /dev/gpt/swap1
```

{% endcut %}

Затирка диска: `dd if=/dev/zero of=/dev/ada0 bs=8M`
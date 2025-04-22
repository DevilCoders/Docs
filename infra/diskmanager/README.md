What
====

diskmanager is host service for disk/LVM management similar to
[openstorage](https://github.com/libopenstorage/openstorage) or
[CSI](https://github.com/container-storage-interface/spec). Service
provides GRPC API for external services, cli client is called
[dmctl](https://a.yandex-team.ru/arc/trunk/arcadia/infra/diskmanager/client).

Assumptions
-----------

-   For the sake of sane reliability, only one disk (physical volume) can be assigned
    to a VolumeGroup, and this disk can not be assigned to another VolumeGroup.
-   Each VolumeGroup has limit on maximum number of LogicalVolumes, for the sake
    of sane latency.
-   Actions idempotence. Each action may be repeated several times.

Build
-----

``` {.example}
# ALWAYS RUN TEST!!!
ya make -t infra/diskmanager
ya make infra/diskmanager
```

Documentation
-------------

Please do not edit this *README.md* file, modify
[doc/README.org](file://README.md) instead

``` {.example}
# Update documentation
cd infra/diskmanager/doc
emacs README.org
sh gendoc.sh
```

Examples
--------

``` {.example}
# Install package
dpkg -i yandex-diskmanager-XX.dpkg
# Ensure that service is running
systemctl start yandex-diskmanager
# Logs are available at /var/log/diskmanager.log

# Basic usage
dmctl disk-list
+------------------------+----------+-------+-------------+------+-------+------------+--------+-------+
|        Disk Id         |   Name   | Class |   Capacity  | UUID | Ready | Configured | Absent | Error |
+------------------------+----------+-------+-------------+------+-------+------------+--------+-------+
| wwn-0x600140536868ea9a | /dev/sdb |  ssd  | 1024.000 Gb |      | False |   False    | False  | False |
| wwn-0x5333333000005dc0 | /dev/sda |  hdd  |  10.000 Gb  |      | False |   False    | False  | False |
+------------------------+----------+-------+-------------+------+-------+------------+--------+-------+

DISK_ID=wwn-0x5333333000005dc0
dmctl disk-format $DISK_ID
+------------------------+----------+-------+-----------+--------------------------------------+-------+------------+--------+-------+
|        Disk Id         |   Name   | Class |  Capacity |                 UUID                 | Ready | Configured | Absent | Error |
+------------------------+----------+-------+-----------+--------------------------------------+-------+------------+--------+-------+
| wwn-0x5333333000005dc0 | /dev/sda |  hdd  | 10.000 Gb | 64fe82f4-8b34-4d87-9d09-49fc70730ec6 |  True |    True    | False  | False |
+------------------------+----------+-------+-----------+--------------------------------------+-------+------------+--------+-------+

VOL_ID=$(./client/dmctl vol-create test-vol $MY_DISK_ID 5G mount --fs_type=ext4)

dmctl vol-mount $VOL_ID /mnt/test-vol
df /mnt/test-vol
Filesystem                                               1K-blocks  Used Available Use% Mounted on
/dev/mapper/diskman--vg--wwn--0x5333333000005dc0-test--vol   5029504 10232   4740744   1% /mnt/test-vol

dmctl vol-umount $VOL_ID
```

Run CI tests via sandbox
------------------------

Sandbox tasks located at
[infra/diskmanager/ci/sandbox-tasks](file://infra/diskmanager/ci/sandbox-tasks)
Use
[sandboxctl](https://a.yandex-team.ru/arc/trunk/arcadia/tools/sandboxctl/README.md)
CLI utility to execute sandbox tasks manually like follows:

``` {.example}
cd infra/diskmanager/ci/sandbox-tasks
# Build package (if not built already)
sandboxctl create -W -i 01-ya_make_package.yml
# Create test image(optional)
## Start async tasks
TASK_ID1=$(sandboxctl create  -i 01-xenial-create-test-image.yml -q)
TASK_ID2=$(sandboxctl create  -i 01-bionic-create-test-image.yml -q)
## Wait task completion
sandboxctl get_task -W $TASK_ID1
sandboxctl get_task -W $TASK_ID2

#Run tests
TASK_ID1=$(sandboxctl create  -i 02-xenial-run-tests.yml -q)
TASK_ID2=$(sandboxctl create  -i 02-bionic-run-tests.yml -q)
## Wait task completion
sandboxctl get_task -W $TASK_ID1
sandboxctl get_task -W $TASK_ID2
```

Release via CI
-----------------

-   [Release page](https://a.yandex-team.ru/projects/infracloudnetwork/ci/releases/timeline?dir=infra%2Fdiskmanager&id=infra-diskmanager-release)
-   File that discribes CI workflows: [a.yaml](a.yaml)

Stats/Metrics
-------------

Diskmanager push stats to
[YASMagent](https://doc.yandex-team.ru/Search/golovan-quickstart) on
localhost with following tags:

``` {.example}
'itype': 'runtimecloud'
```

Check [panel](https://yasm.yandex-team.ru/template/panel/rtc_diskman) for cluster status.

### Exported values

|Value name                             |Description                            |
|---------------------------------------|---------------------------------------|
|push-diskmanager~fstrimbytesdhhh~      |Bytes fstrimmed                        |
|push-diskmanager~fstrimerrorsdhhh~     |Errors during fstrim                   |
|push-diskmanager~nrdisksahhh~          |Number of disks diskman know about     |
|push-diskmanager~nrdisksreadyahhh~     |Number of disks in ready state         |
|push-diskmanager~nrvolumesahhh~        |Number of volumes                      |
|push-diskmanager~nrvolumesmountsahhh~  |Number of mounted volumes              |
|push-diskmanager~nrvolumesreadyahhh~   |Number of folumes in ready state       |
|push-diskmanager~volumessizeGBahhh~    |Total size of volumes allocated in GB  |

Integration
===========

Deploy service (setup.yandex-team.ru)
-------------------------------------

Deploy nodes with LVM partition scheme and tag disks with diskman's tags

-   each disk has diskman=true
-   each system volume has: diskman.sys=true (root,place,home)

### Default configs available

rtc-dm-ubuntu-16.04
:   <https://setup.yandex-team.ru/#!/configs/view/rtc-dm-ubuntu-16.04>

# Yocto-слои для сборки образа для nanopi-neo4

## Сборка в Sandbox
Для сборки в Sandbox нужно воспользоваться задачей `MAPS_MRC_DRIVE_NANOPI_IMAGE_BUILD_TASK`.
Код задачи живет [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/mrc/MapsMrcDriveNanopiImageBuildTask).

## Самостоятельная сборка
Для сборки используются сторонние meta-слои `poky`, `meta-openembedded`, `meta-rockchip`, `meta-rauc`, а также BSP-слой `meta-nanopi-neo4` и слой `meta-mrc`, хранящиеся в Аркадии.

### Требования
1. Машина с ubuntu xenial или bionic.
2. 50 Гб свободного места на диске.
3. Установленные пакеты: `diffstat`, `unzip`, `chrpath`, `autoconf`, `automake`, `libtool`, `patchutils`, `texinfo`.

### Инструкция
1. Выбираем рабочую директорию и создаем в ней папку `sources`:
    `$ mkdir sources && cd sources`

2. Создаем симлинки на слои из Аркадии и конфиги для сборки:
    `$ ln -s $(ARCADIA_ROOT)/maps/wikimap/mapspro/services/mrc/drive/mobile/yocto/meta-nanopi-neo4 meta-nanopi-neo4`
    `$ ln -s $(ARCADIA_ROOT)/maps/wikimap/mapspro/services/mrc/drive/mobile/yocto/meta-mrc meta-mrc`
    `$ ln -s $(ARCADIA_ROOT)/maps/wikimap/mapspro/services/mrc/drive/mobile/yocto/conf conf`
    `$ ln -s $(ARCADIA_ROOT)/maps/wikimap/mapspro/services/mrc/drive/mobile/yocto/scripts scripts`

3. Скачиваем сторонние слои
    `$ git clone https://github.com/openembedded/meta-openembedded.git`
    `$ git clone git://git.yoctoproject.org/poky`
    `$ git clone git://git.yoctoproject.org/meta-rockchip`
    `$ git clone https://github.com/rauc/meta-rauc.git`

В склонированных репозиториях переходим на следующие коммиты:
```
meta-openembedded:  8760facba1bceb299b3613b8955621ddaa3d4c3f
poky:               cbb677e9a09d5dad34404a851f7c23aeb5122465
meta-rockchip:      e3b22570d7e4411ba72d01f4ff87c1cc5a48824d
meta-rauc:          09cc4d298e84257cc5fc30ea8721090cdae4a315
```

4. Настраиваем окружение
Из рабочей директории (в которой находится папка `sources`) выполняем
    `$ ln -s sources/scripts/setup-environment.sh`
    `$ MACHINE=nanopi-neo4 DISTRO=rk-none ARCADIA=/path/to/arcadia source ./setup-environment.sh build`
После выполнения этого шага мы окажемся в папке `build`.

5. Запускаем сборку
Для сборки прошивки в testing:
    `$ bitbake rk-image-drive-testing`
Для сборки прошивки в stable:
    `$ bitbake rk-image-drive-stable`

Первичная сборка может занять продолжительное время.

### Warning
В `sandbox` сейчас используется уже скачанный репозиторий `meta-rockchip`, который на текущий момент уже удален из `github`.
Поэтому sandbox-сборка и сборка по данной инструкции потенциально могут отличаться.
На данный момент различий между функциональностью образов не выявлено.

## Прошивка образа на устройство
В результате сборки образы появятся в `build/tmp/deploy/images/nanopi-neo4/`.

### Первоначальная прошивка
Для первоначальной прошивки nanopi используются файлы `rk-image-drive-${staging}-nanopi-neo4.wic.bz2` и `rk-image-drive-${staging}-nanopi-neo4.wic.bmap`.
Для прошивки eMMC нужно загрузиться с SD-карты, на которую заранее скопированы два указанных файла, и прошить eMMC утилитой `bmaptool`:
    `$ sudo bmaptool copy rk-image-drive-${staging}-nanopi-neo4.wic.bz2 /dev/mmcblkX`
где вместо `mmcblkX` подставить девайс, под которым определилась eMMC (можно узнать через `lsblk`, обычно `mmcblk1`).

В образ добавлены два пользователя: `mrc` и `root`. Пароли к этим пользователям определены в секретнице и зависят от `staging`.

### Обновление rootfs
Для обновления `rootfs`-раздела используется файл `rk-image-drive-${staging}-nanopi-neo4.ext4`.
Обновить раздел вручную можно с помощью утилиты `dd` или `dcfldd`.

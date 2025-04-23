# Сборка delta слоя YT для Nanny сервисов

- Общее описание
- infra/environments/yt
- sandbox/projects/porto/common/resource_types.py
- Таска в sandbox
- Настройка в Nanny сервисе


## Общее описание
Для YT мы собираем дельту относительно стандартных app образов rtc (app - минимальные образы для porto с virt_mode=app).
Сборка выполняется таской sandbox YA_MAKE_TGZ.


## infra/environments/yt
Под нужную версию ubuntu заводится подкаталог с такой структурой.

bionic/ya.make
bionic/config.inc
bionic/script
bionic/script/00_prepare_apt.sh
bionic/script/90_check_apt_state.sh
bionic/script/91_cleanup_apt.sh
bionic/script/92_cleanup_tmp.sh
bionic/script/99_tests.sh
bionic/script/SHA1SUMS

### bionic/ya.make
INCLUDE(config.inc) - добавляется конфиг дельты.
INCLUDE(${ARCADIA_ROOT}/infra/environments/lib/porto-layer.inc) - и общий конфиг для слоев RTC.

### bionic/config.inc
В конфиге указывается несколько важных переменных окружения:
- ENV_BASE_DIR - должна указывать на каталог с дельтой (infra/environments/yt/bionic)
- BASE_LAYER_DIR - путь к базовому слою, относительно которого собирается дельта (infra/environments/rtc-base-bionic/release/app-layer)
- ENV_LAYER_NAME - указываем имя файла с дельта слоем.

### bionic/script/00_prepare_apt.sh bionic/script/9X
Эти скрипты лучше оставить, как есть, и свои добавлять в отдельные файлы > 00_, < 90_. 
bionic/script/99_tests.sh - это файл для тестов, в нем можно собрать проверки корректности сборки слоя, что нужные пакеты поставились, есть нужные файлы и тп.

### bionic/script/SHA1SUMS
SHA1 суммы скриптов.


## sandbox/projects/porto/common/resource_types.py
Для того, чтобы мы могли релизить таски YA_MAKE_TGZ, заведен отдельный тип ресурсов - PORTO_LAYER_YT .
В качестве releasers прописана sandbox группа YT_ROBOT.


## таска YA_MAKE_TGZ
В "Build artifacts" нужно прописать путь до делта слоя, это путь в arcadia + ENV_LAYER_NAME - infra/environments/yt/bionic/diff.tar.zst .
В "Targets" нужно прописать путь до дельты - infra/environments/yt/bionic .
A для того, чтобы можно было релизить, нужно указать в опции "Result resource type" выходной тип ресурса - PORTO_LAYER_YT .


## Настройка в Nanny сервисе
В instance spec в "List of layers to assemble instance FS" сперва нужно добавить базовый слой, через "Choose Bottom Layer",
после чего указать в ресурс дельты.

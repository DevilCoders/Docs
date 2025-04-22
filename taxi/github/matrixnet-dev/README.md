# libyandex-taxi-matrixnet

## Build on xenial
1) `make`

## Build on bionic
1) `test -f /usr/include/xlocale.h || ln -s /usr/include/locale.h /usr/include/xlocale.h`
     (https://ahelpme.com/linux/compiling/glibc-2-26-and-failure-to-compile-because-of-xlocale-h/)
1) `make`

## Build bionic version on xenial in Docker
1) allow SSH access to Arcadia from container (https://wiki.yandex-team.ru/taxi/backend/automatization/pamjatka-bojjca-avtomatizacii/#ssh-to-vm-to-docker)
1) `test -f /usr/include/xlocale.h || ln -s /usr/include/locale.h /usr/include/xlocale.h`
     (https://ahelpme.com/linux/compiling/glibc-2-26-and-failure-to-compile-because-of-xlocale-h/)
2) `make`

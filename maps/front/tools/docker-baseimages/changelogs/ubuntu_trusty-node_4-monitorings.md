## 4.2.0

 * [b92dcf9](https://github.yandex-team.ru/maps/docker-baseimages/commit/b92dcf9) Use include.d/ instead of include/
 * [6031d33](https://github.yandex-team.ru/maps/docker-baseimages/commit/6031d33) Revert "MAPSINFRA-761 Using node.js builds from NodeSource (#112)"
 * [7dd6197](https://github.yandex-team.ru/maps/docker-baseimages/commit/7dd6197) MAPSINFRA-761 Using node.js builds from NodeSource (#112)
 * [e41fa5e](https://github.yandex-team.ru/maps/docker-baseimages/commit/e41fa5e) MAPSINFRA-619 Implementing close/open web host functionality (#113)

## 4.1.0

 * [e39dda4](https://github.yandex-team.ru/maps/docker-baseimages/commit/e39dda4) Using vanilla:2.3.1 in monitorings
 * [08a2633](https://github.yandex-team.ru/maps/docker-baseimages/commit/08a2633) Use ENV instruction to passing vars to start.sh (#111)
 * [366744b](https://github.yandex-team.ru/maps/docker-baseimages/commit/366744b) Specify exec form for CMD command in monitorings image README (#110)

## 4.0.1

 * [dda4fb6](https://github.yandex-team.ru/maps/docker-baseimages/commit/dda4fb6) Using vanilla:2.2.1
 * [bb002f5](https://github.yandex-team.ru/maps/docker-baseimages/commit/bb002f5) exec supervisord in start.sh (#107)

## 4.0.0

 * [42e97e6](https://github.yandex-team.ru/maps/docker-baseimages/commit/42e97e6) Set the default path to the application to /usr/local/app
 * [60acc67](https://github.yandex-team.ru/maps/docker-baseimages/commit/60acc67) Use a newer version of the vanilla image (includes vim and node 8.14)
 * [29113b2](https://github.yandex-team.ru/maps/docker-baseimages/commit/29113b2) Add tcpdump and strace (#102)

## 3.5.0

 * [71d5803](https://github.yandex-team.ru/maps/docker-baseimages/commit/71d5803) Added yandex-internal-ca to the monitorings image

## 3.4.4

 * [ed5731d](https://github.yandex-team.ru/maps/docker-baseimages/commit/ed5731d) Updated the vanilla baseimage used in monitorings to 2.0.2

## 3.4.3

 * [487f2e5](https://github.yandex-team.ru/maps/docker-baseimages/commit/487f2e5) MAPSINFRA-524: Пофиксить мониторинг node_worker

## 3.4.2

 * [45bc050](https://github.yandex-team.ru/maps/docker-baseimages/commit/45bc050) Bumped the version of the vanilla image in the monitorings image

## 3.4.1

 * [23147dd](https://github.yandex-team.ru/maps/docker-baseimages/commit/23147dd) Fixing subshell call for trusty

## 3.4.0

 * [5add462](https://github.yandex-team.ru/maps/docker-baseimages/commit/5add462) Added /etc/baseimage.name to the monitorings flavor
 * [929867c](https://github.yandex-team.ru/maps/docker-baseimages/commit/929867c) Monitorings README: use supervisorctl cmd for check status of processes (#94)

## 3.3.0

 * [88fc3e6](https://github.yandex-team.ru/maps/docker-baseimages/commit/88fc3e6) MAPSINFRA-419: Сохранять версию базового образа в самом образе (#93)

## 3.2.3

 * [02bbbbf](https://github.yandex-team.ru/maps/docker-baseimages/commit/02bbbbf) Morbid.fix dir create (#90)
 * [91801c4](https://github.yandex-team.ru/maps/docker-baseimages/commit/91801c4) create project dir for remove warning (#88)

## 3.2.2

 * [7911a6e](https://github.yandex-team.ru/maps/docker-baseimages/commit/7911a6e) create project dir for remove warning

## 3.2.1

 * [e7d3dda](https://github.yandex-team.ru/maps/docker-baseimages/commit/e7d3dda) Make the monitorings image restartable (#87)
 * [639611f](https://github.yandex-team.ru/maps/docker-baseimages/commit/639611f) Move the monitorings to ubuntu-node/flavors/monitorings (#84)

## 3.2.0

 * [0cc28e8](https://github.yandex-team.ru/maps/docker-baseimages/commit/0cc28e8) Add ssl cert check (#82)

## 3.1.1

 * [93bc7b0](https://github.yandex-team.ru/maps/docker-baseimages/commit/93bc7b0) fix node_worker_check (#77)

## 3.1.0

 * [6ceebd1](https://github.yandex-team.ru/maps/docker-baseimages/commit/6ceebd1) replace sed with full conf (#75)
 * [d3329c2](https://github.yandex-team.ru/maps/docker-baseimages/commit/d3329c2) Added MAPS_NODEJS_OPTIONS variable for ubuntu-node/flavors/monitorings. Fixes #64

## 3.0.0

 * [f2acf17](https://github.yandex-team.ru/maps/docker-baseimages/commit/f2acf17) nginx: Remove X-Forwarded-Host and X-Forwarded-For headers (#63)

## 2.1.0

 * [71fcba1](https://github.yandex-team.ru/maps/docker-baseimages/commit/71fcba1) Morbid.fix node monitoring (#61)

## 2.1.0

 * [551a0d0](https://github.yandex-team.ru/maps/docker-baseimages/commit/551a0d0) Add custom monitorings (#55)

## 2.0.0

 * [d1e4a52](https://github.yandex-team.ru/maps/docker-baseimages/commit/d1e4a52) Using the vanilla image without yarn in monitorings

## 1.0.0

 * [5a60935](https://github.yandex-team.ru/maps/docker-baseimages/commit/5a60935) Moved the nginx-logging image to ubuntu-node/flavors/monitorings

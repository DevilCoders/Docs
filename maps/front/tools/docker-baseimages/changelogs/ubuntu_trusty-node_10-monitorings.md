## 1.2.0

 * [c9ac6fd](https://github.yandex-team.ru/maps/docker-baseimages/commit/c9ac6fd) fix roquefort pkg name

## 1.1.0

 * [24f0203](https://github.yandex-team.ru/maps/docker-baseimages/commit/24f0203) MAPSINFRA-781: add motd screen on login (#120)
 * [7835b3c](https://github.yandex-team.ru/maps/docker-baseimages/commit/7835b3c) Add tools for control instance from balancers (#119)
 * [9706906](https://github.yandex-team.ru/maps/docker-baseimages/commit/9706906) Add roquefort & unistat-proxy (#118)
 * [7fcbcf4](https://github.yandex-team.ru/maps/docker-baseimages/commit/7fcbcf4) Added net-tools to monitorings
 * [3550de4](https://github.yandex-team.ru/maps/docker-baseimages/commit/3550de4) Add missing folders for juggler
 * [ce9288f](https://github.yandex-team.ru/maps/docker-baseimages/commit/ce9288f) Ensure tzdata is included in the image
 * [e10e471](https://github.yandex-team.ru/maps/docker-baseimages/commit/e10e471) Fix cron errors in the monitorings flavor (#117)
 * [894530e](https://github.yandex-team.ru/maps/docker-baseimages/commit/894530e) Removing syslog from nginx logging
 * [fc0559d](https://github.yandex-team.ru/maps/docker-baseimages/commit/fc0559d) Using the freshly built xenial images
 * [87184f1](https://github.yandex-team.ru/maps/docker-baseimages/commit/87184f1) Revert "Revert "MAPSINFRA-761 Using node.js builds from NodeSource (#112)""
 * [b92dcf9](https://github.yandex-team.ru/maps/docker-baseimages/commit/b92dcf9) Use include.d/ instead of include/
 * [6031d33](https://github.yandex-team.ru/maps/docker-baseimages/commit/6031d33) Revert "MAPSINFRA-761 Using node.js builds from NodeSource (#112)"
 * [7dd6197](https://github.yandex-team.ru/maps/docker-baseimages/commit/7dd6197) MAPSINFRA-761 Using node.js builds from NodeSource (#112)
 * [e41fa5e](https://github.yandex-team.ru/maps/docker-baseimages/commit/e41fa5e) MAPSINFRA-619 Implementing close/open web host functionality (#113)
 * [e39dda4](https://github.yandex-team.ru/maps/docker-baseimages/commit/e39dda4) Using vanilla:2.3.1 in monitorings
 * [08a2633](https://github.yandex-team.ru/maps/docker-baseimages/commit/08a2633) Use ENV instruction to passing vars to start.sh (#111)
 * [366744b](https://github.yandex-team.ru/maps/docker-baseimages/commit/366744b) Specify exec form for CMD command in monitorings image README (#110)
 * [dda4fb6](https://github.yandex-team.ru/maps/docker-baseimages/commit/dda4fb6) Using vanilla:2.2.1
 * [bb002f5](https://github.yandex-team.ru/maps/docker-baseimages/commit/bb002f5) exec supervisord in start.sh (#107)
 * [42e97e6](https://github.yandex-team.ru/maps/docker-baseimages/commit/42e97e6) Set the default path to the application to /usr/local/app
 * [60acc67](https://github.yandex-team.ru/maps/docker-baseimages/commit/60acc67) Use a newer version of the vanilla image (includes vim and node 8.14)

## 1.0.0

 * [29113b2](https://github.yandex-team.ru/maps/docker-baseimages/commit/29113b2) Add tcpdump and strace (#102)
 * [71d5803](https://github.yandex-team.ru/maps/docker-baseimages/commit/71d5803) Added yandex-internal-ca to the monitorings image
 * [ed5731d](https://github.yandex-team.ru/maps/docker-baseimages/commit/ed5731d) Updated the vanilla baseimage used in monitorings to 2.0.2
 * [487f2e5](https://github.yandex-team.ru/maps/docker-baseimages/commit/487f2e5) MAPSINFRA-524: Пофиксить мониторинг node_worker
 * [45bc050](https://github.yandex-team.ru/maps/docker-baseimages/commit/45bc050) Bumped the version of the vanilla image in the monitorings image
 * [5add462](https://github.yandex-team.ru/maps/docker-baseimages/commit/5add462) Added /etc/baseimage.name to the monitorings flavor
 * [929867c](https://github.yandex-team.ru/maps/docker-baseimages/commit/929867c) Monitorings README: use supervisorctl cmd for check status of processes (#94)
 * [88fc3e6](https://github.yandex-team.ru/maps/docker-baseimages/commit/88fc3e6) MAPSINFRA-419: Сохранять версию базового образа в самом образе (#93)
 * [02bbbbf](https://github.yandex-team.ru/maps/docker-baseimages/commit/02bbbbf) Morbid.fix dir create (#90)
 * [91801c4](https://github.yandex-team.ru/maps/docker-baseimages/commit/91801c4) create project dir for remove warning (#88)
 * [e7d3dda](https://github.yandex-team.ru/maps/docker-baseimages/commit/e7d3dda) Make the monitorings image restartable (#87)
 * [639611f](https://github.yandex-team.ru/maps/docker-baseimages/commit/639611f) Move the monitorings to ubuntu-node/flavors/monitorings (#84)
 * [6ceebd1](https://github.yandex-team.ru/maps/docker-baseimages/commit/6ceebd1) replace sed with full conf (#75)
 * [d3329c2](https://github.yandex-team.ru/maps/docker-baseimages/commit/d3329c2) Added MAPS_NODEJS_OPTIONS variable for ubuntu-node/flavors/monitorings. Fixes #64
 * [f2acf17](https://github.yandex-team.ru/maps/docker-baseimages/commit/f2acf17) nginx: Remove X-Forwarded-Host and X-Forwarded-For headers (#63)
 * [71fcba1](https://github.yandex-team.ru/maps/docker-baseimages/commit/71fcba1) Morbid.fix node monitoring (#61)
 * [551a0d0](https://github.yandex-team.ru/maps/docker-baseimages/commit/551a0d0) Add monitorings (#55)
 * [56d6350](https://github.yandex-team.ru/maps/docker-baseimages/commit/56d6350) Fixing the LFs in ubuntu-node/flavors/monitorings/README.md
 * [ea62bf9](https://github.yandex-team.ru/maps/docker-baseimages/commit/ea62bf9) Обновление основного README.md (#56)
 * [d1e4a52](https://github.yandex-team.ru/maps/docker-baseimages/commit/d1e4a52) Using the vanilla image without yarn in monitorings
 * [d731c55](https://github.yandex-team.ru/maps/docker-baseimages/commit/d731c55) Grammar fixes
 * [7d23904](https://github.yandex-team.ru/maps/docker-baseimages/commit/7d23904) Templating flavors/monitoring
 * [5a60935](https://github.yandex-team.ru/maps/docker-baseimages/commit/5a60935) Moved the nginx-logging image to ubuntu-node/flavors/monitorings
 * [b9b32a2](https://github.yandex-team.ru/maps/docker-baseimages/commit/b9b32a2) Removing the dummy file from flavors/monitorings
 * [a4e0778](https://github.yandex-team.ru/maps/docker-baseimages/commit/a4e0778) More robust versioning (#48)


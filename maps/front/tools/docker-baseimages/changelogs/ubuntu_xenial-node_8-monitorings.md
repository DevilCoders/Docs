## 10.3.8

 * [112bdeb](https://github.yandex-team.ru/maps/docker-baseimages/commit/112bdeb) use close instead of exit to fully read stdout; (#210)

## 10.3.7

 * [4f32a5e](https://github.yandex-team.ru/maps/docker-baseimages/commit/4f32a5e) MAPSINFRA-2295: reduce nginx worker to 2 (#209)

## 10.3.6

 * [3003f48](https://github.yandex-team.ru/maps/docker-baseimages/commit/3003f48) FIX: return MAPS_DEPLOY_UNIT for Qloud platform

## 10.3.5

 * [5cc6302](https://github.yandex-team.ru/maps/docker-baseimages/commit/5cc6302) MAPSINFRA-2244: portoclt & ssl/ca (#208)

## 10.3.4

 * [bac8fef](https://github.yandex-team.ru/maps/docker-baseimages/commit/bac8fef) add nee dev-domain

## 10.3.3

 * [c835abb](https://github.yandex-team.ru/maps/docker-baseimages/commit/c835abb) MAPSINFRA-2194: add *.deneb.maps.dev.yandex.TLD to local crt (#207)

## 10.3.2

 * [3a79d43](https://github.yandex-team.ru/maps/docker-baseimages/commit/3a79d43) [Deploy] Fixed MAPS_LOGBROKER_TOPIC

## 10.3.1

 * [885587a](https://github.yandex-team.ru/maps/docker-baseimages/commit/885587a) MAPSINFRA-2093: fixed `hard` argument

## 10.3.0

 * [d7c1214](https://github.yandex-team.ru/maps/docker-baseimages/commit/d7c1214) MAPSINFRA-2093: [Deploy] Graceful degradation

## 10.2.3

 * [f6b3bfe](https://github.yandex-team.ru/maps/docker-baseimages/commit/f6b3bfe) Update motd
 * [2a8cdf6](https://github.yandex-team.ru/maps/docker-baseimages/commit/2a8cdf6) Update start.sh
 * [dfaab63](https://github.yandex-team.ru/maps/docker-baseimages/commit/dfaab63) Update accesslog-tskv.template.conf

## 10.2.2

 * [508f30c](https://github.yandex-team.ru/maps/docker-baseimages/commit/508f30c) fix start.sh
 * [842fa17](https://github.yandex-team.ru/maps/docker-baseimages/commit/842fa17) fix roquefort-custom supervisor.conf
 * [67892b4](https://github.yandex-team.ru/maps/docker-baseimages/commit/67892b4) Update accesslog-tskv.template.conf

## 10.2.1

 * [6e85527](https://github.yandex-team.ru/maps/docker-baseimages/commit/6e85527) Update common-env-values.sh
 * [59641db](https://github.yandex-team.ru/maps/docker-baseimages/commit/59641db) fix start.sh

## 10.2.0

 * [38e8428](https://github.yandex-team.ru/maps/docker-baseimages/commit/38e8428) MAPSINFRA-1986: Unified baseimage (#203)
 * [c3e49a3](https://github.yandex-team.ru/maps/docker-baseimages/commit/c3e49a3) MAPSINFRA-1476: turn off proxy_intercept_errors (#204)

## 10.1.4

 * [6ed7325](https://github.yandex-team.ru/maps/docker-baseimages/commit/6ed7325) MAPSINFRA-1981: [base-image] Убрать ограничение с ручки /close

## 10.1.3

 * [ee2a9a7](https://github.yandex-team.ru/maps/docker-baseimages/commit/ee2a9a7) MAPSINFRA-1847: Добавить jq в базовый образ
 * [5e1560e](https://github.yandex-team.ru/maps/docker-baseimages/commit/5e1560e) MAPSINFRA-1914: Update prepare-roquefort.js

## 10.1.2

 * [6a3dc0f](https://github.yandex-team.ru/maps/docker-baseimages/commit/6a3dc0f) Pass original "host" header if possible (#197)

## 10.1.1

 * [b269d91](https://github.yandex-team.ru/maps/docker-baseimages/commit/b269d91) fix DEV mode

## 10.1.0

 * [18a2a3a](https://github.yandex-team.ru/maps/docker-baseimages/commit/18a2a3a) MAPSINFRA-1082: add dev-https to baseimage (#195)

## 10.0.1

 * [e030a6f](https://github.yandex-team.ru/maps/docker-baseimages/commit/e030a6f) Не использовать дефолтный лог для кастомного рокфора

## 10.0.0

 * [988ff3d](https://github.yandex-team.ru/maps/docker-baseimages/commit/988ff3d) Turning off services by deleting symlinks (#194)
 * [2f745f7](https://github.yandex-team.ru/maps/docker-baseimages/commit/2f745f7) MAPSINFRA-1485: Причесать документацию в docker-baseimages

## 9.0.1

 * [6a549b9](https://github.yandex-team.ru/maps/docker-baseimages/commit/6a549b9) Fix app boot (#192)
 * [92caa4e](https://github.yandex-team.ru/maps/docker-baseimages/commit/92caa4e) MAPSINFRA-1488: Убить vanilla базовый образ

## 9.0.0

 * [b0b7c01](https://github.yandex-team.ru/maps/docker-baseimages/commit/b0b7c01) MAPSINFRA-1487: split one file into many (#175)

## 8.1.9

 * [7aed401](https://github.yandex-team.ru/maps/docker-baseimages/commit/7aed401) Using vanilla:4.0.3

## 8.1.8

 * [7f112e3](https://github.yandex-team.ru/maps/docker-baseimages/commit/7f112e3) Using vanilla:4.0.2
 * [acaab6d](https://github.yandex-team.ru/maps/docker-baseimages/commit/acaab6d) [monitorings] Fix roquefort logrotate for trusty (#186)

## 8.1.7

 * [ce1a945](https://github.yandex-team.ru/maps/docker-baseimages/commit/ce1a945) [monitorings]: Add logrotate config for roquefort-custom.log (#185)
 * [c2bc34a](https://github.yandex-team.ru/maps/docker-baseimages/commit/c2bc34a) README.monitorings.md: Actualize custom signals instructions

## 8.1.6

 * [7e09785](https://github.yandex-team.ru/maps/docker-baseimages/commit/7e09785) [monitorings]: Specify --logs-to-stderr for roquefort-custom (#184)
 * [67cc223](https://github.yandex-team.ru/maps/docker-baseimages/commit/67cc223) Fix killing of cutom check processes (#183)

## 8.1.5

 * [46c718b](https://github.yandex-team.ru/maps/docker-baseimages/commit/46c718b) MAPSINFRA-1215 Добавить поддержку окружений в prepare-roquefort.js
 * [5b04e0d](https://github.yandex-team.ru/maps/docker-baseimages/commit/5b04e0d) Add docs about custom logs and checks

## 8.1.4

 * [895c734](https://github.yandex-team.ru/maps/docker-baseimages/commit/895c734) MAPSINFRA-1493 Ручка для отдачи .qtools.json

## 8.1.3

 * [3217ce1](https://github.yandex-team.ru/maps/docker-baseimages/commit/3217ce1) Remove .gitkeep in Dockerfile

## 8.1.2

 * No changes

## 8.1.1

 * No changes

## 8.1.0

 * [34c7eb6](https://github.yandex-team.ru/maps/docker-baseimages/commit/34c7eb6) MAPSINFRA-1179: [Monitorings] Тулза для собра кастомных сигналов c инстанса
 * [7669d71](https://github.yandex-team.ru/maps/docker-baseimages/commit/7669d71) MAPSINFRA-1177: [Monitorings] Добавить поддержку кастомных графиков в базовый образ
 * [c5252e4](https://github.yandex-team.ru/maps/docker-baseimages/commit/c5252e4) MAPSINFRA-1480: Перенести инструментов сборки ubuntu-node образа в корень репозитории (#176)

## 8.0.1

 * [81443e4](https://github.yandex-team.ru/maps/docker-baseimages/commit/81443e4) update monitoring-utils package version

## 8.0.0

 * [e5ca701](https://github.yandex-team.ru/maps/docker-baseimages/commit/e5ca701) MAPSINFRA-1175: remove dorblu & config (#174)
 * [d07e702](https://github.yandex-team.ru/maps/docker-baseimages/commit/d07e702) MAPSINFRA-1174: Add script to work with paste.yandex-team.ru (#171)

## 7.2.1

 * [c4d70b0](https://github.yandex-team.ru/maps/docker-baseimages/commit/c4d70b0) MAPSINFRA-1225: fix locales (#173)

## 7.2.0

 * [9a29919](https://github.yandex-team.ru/maps/docker-baseimages/commit/9a29919) Update yandex-int/maps._monitoring-utils to 0.1.0 (#169)
 * [342a502](https://github.yandex-team.ru/maps/docker-baseimages/commit/342a502) README: add doc for extend.start.sh (#168)
 * [590f652](https://github.yandex-team.ru/maps/docker-baseimages/commit/590f652) Fix typo in /usr/local/tool/convert-to-roquefort.js error message (#167)

## 7.1.0

 * [e63f5eb](https://github.yandex-team.ru/maps/docker-baseimages/commit/e63f5eb) Add the ability to run additional command/scripts (#160)

## 7.0.1

 * [2854004](https://github.yandex-team.ru/maps/docker-baseimages/commit/2854004) Using monitoring-utils@0.0.12

## 7.0.0

 * [e64d56d](https://github.yandex-team.ru/maps/docker-baseimages/commit/e64d56d) Added an empty line to build a new version

## 6.2.5

 * [581d4da](https://github.yandex-team.ru/maps/docker-baseimages/commit/581d4da) Fixed convert-to-roquefort and prepare-roquefort-config

## 6.2.4

 * [c4845a2](https://github.yandex-team.ru/maps/docker-baseimages/commit/c4845a2) Using monitoring-utils package v0.0.8
 * [3373d6b](https://github.yandex-team.ru/maps/docker-baseimages/commit/3373d6b) Monitoring fixes (#164)

## 6.2.3

 * [983a25f](https://github.yandex-team.ru/maps/docker-baseimages/commit/983a25f) Обновить парсилку рокфора (#163)
 * [21593a6](https://github.yandex-team.ru/maps/docker-baseimages/commit/21593a6) Prettify roquefort/extended.conf (#161)

## 6.2.2

 * No changes

## 6.2.1

 * [23d504a](https://github.yandex-team.ru/maps/docker-baseimages/commit/23d504a) Use -t stable on apt install

## 6.2.0

 * [9f0d812](https://github.yandex-team.ru/maps/docker-baseimages/commit/9f0d812) Fixed a typo in the Dockerfile
 * [87de2c3](https://github.yandex-team.ru/maps/docker-baseimages/commit/87de2c3) Use vanilla:4.0.1
 * [14de945](https://github.yandex-team.ru/maps/docker-baseimages/commit/14de945) MAPSINFRA-691: change push-client config for send log to standalone folder (#147)
 * [8635653](https://github.yandex-team.ru/maps/docker-baseimages/commit/8635653) MAPSINFRA-1080 maps_init + convert-to-roquefort (#159)
 * [a8f951b](https://github.yandex-team.ru/maps/docker-baseimages/commit/a8f951b) Fix monitorings build (#158)
 * [b0d8ff9](https://github.yandex-team.ru/maps/docker-baseimages/commit/b0d8ff9) Remove all MAPS_NODEJS_APP defaults from README (#156)

## 6.1.4

 * [5bc889b](https://github.yandex-team.ru/maps/docker-baseimages/commit/5bc889b) Setting the permissions after copying the files

## 6.1.3

 * [c2d6cc7](https://github.yandex-team.ru/maps/docker-baseimages/commit/c2d6cc7) Yet another logrotate fix (#151)

## 6.1.2

 * [a2754e0](https://github.yandex-team.ru/maps/docker-baseimages/commit/a2754e0) Reintroducing logrotate-hourly (#150)

## 6.1.1

 * [bb99dd0](https://github.yandex-team.ru/maps/docker-baseimages/commit/bb99dd0) Use ubuntu's logrotate build (#145)

## 6.1.0

 * [2454e6d](https://github.yandex-team.ru/maps/docker-baseimages/commit/2454e6d) Disable pam_limits(cron:session) messages (#138)

## 6.0.3

 * [22a3b1e](https://github.yandex-team.ru/maps/docker-baseimages/commit/22a3b1e) fix localce & cron logging (#131)
 * [e60503b](https://github.yandex-team.ru/maps/docker-baseimages/commit/e60503b) Fix typo and command name in motd (#130)

## 6.0.2

 * [2634a87](https://github.yandex-team.ru/maps/docker-baseimages/commit/2634a87) Add less to monitorings image (#127)
 * [5dcccf6](https://github.yandex-team.ru/maps/docker-baseimages/commit/5dcccf6) Fix roquefort logs (#126)

## 6.0.1

 * [0705bc9](https://github.yandex-team.ru/maps/docker-baseimages/commit/0705bc9) Add lsof and psmisc utils to monitorings

## 6.0.0

 * [c99b57d](https://github.yandex-team.ru/maps/docker-baseimages/commit/c99b57d) Fix build for monitorings
 * [abba98d](https://github.yandex-team.ru/maps/docker-baseimages/commit/abba98d) Use vanilla:4.0.0
 * [c1e4e12](https://github.yandex-team.ru/maps/docker-baseimages/commit/c1e4e12) Move yandex repos to monitorings(#125)
 * [1f86904](https://github.yandex-team.ru/maps/docker-baseimages/commit/1f86904) Fix logrotate (GEOMONITORINGS-6267) (#124)
 * [908c9ca](https://github.yandex-team.ru/maps/docker-baseimages/commit/908c9ca) Remove MAPS_NODEJS_APP default (#122)
 * [aa63ce7](https://github.yandex-team.ru/maps/docker-baseimages/commit/aa63ce7) fix typo in bash.bashrc
 * [6901eee](https://github.yandex-team.ru/maps/docker-baseimages/commit/6901eee) Fix monitorings build
 * [c9ac6fd](https://github.yandex-team.ru/maps/docker-baseimages/commit/c9ac6fd) fix roquefort pkg name

## 5.1.0

 * [24f0203](https://github.yandex-team.ru/maps/docker-baseimages/commit/24f0203) MAPSINFRA-781: add motd screen on login (#120)
 * [7835b3c](https://github.yandex-team.ru/maps/docker-baseimages/commit/7835b3c) Add tools for control instance from balancers (#119)
 * [9706906](https://github.yandex-team.ru/maps/docker-baseimages/commit/9706906) Add roquefort & unistat-proxy (#118)
 * [7fcbcf4](https://github.yandex-team.ru/maps/docker-baseimages/commit/7fcbcf4) Added net-tools to monitorings

## 5.0.3

 * [3550de4](https://github.yandex-team.ru/maps/docker-baseimages/commit/3550de4) Add missing folders for juggler

## 5.0.2

 * [ce9288f](https://github.yandex-team.ru/maps/docker-baseimages/commit/ce9288f) Ensure tzdata is included in the image
 * [e10e471](https://github.yandex-team.ru/maps/docker-baseimages/commit/e10e471) Fix cron errors in the monitorings flavor (#117)

## 5.0.1

 * [894530e](https://github.yandex-team.ru/maps/docker-baseimages/commit/894530e) Removing syslog from nginx logging

## 5.0.0

 * No changes


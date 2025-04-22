## 3.1.1

 * [043b39a](https://github.yandex-team.ru/maps/docker-baseimages/commit/043b39a) update motd (#237)

## 3.1.0

 * [cc2739a](https://github.yandex-team.ru/maps/docker-baseimages/commit/cc2739a) add push-clien authorization; fix push-clien graph (#236)
 * [98244da](https://github.yandex-team.ru/maps/docker-baseimages/commit/98244da) MAPSINFRA-3354: add signal from push-client (#234)
 * [6949737](https://github.yandex-team.ru/maps/docker-baseimages/commit/6949737) fix detach.sh (#235)

## 3.0.1

 * [a7c42da](https://github.yandex-team.ru/maps/docker-baseimages/commit/a7c42da) fix new baseimages (#233)

## 3.0.0

 * [9e08381](https://github.yandex-team.ru/maps/docker-baseimages/commit/9e08381) MAPSINFRA-3313: instancectl: переписать все команды на js (#228)
 * [3a3ee7d](https://github.yandex-team.ru/maps/docker-baseimages/commit/3a3ee7d) MAPSINFRA-3319: Replace x-forwarded-for by x-forwaded-for-y (#231)
 * [95ed7c4](https://github.yandex-team.ru/maps/docker-baseimages/commit/95ed7c4) MAPSINFRA-3246: Залочить версию nodejs в базовом образе (#223)
 * [cfee048](https://github.yandex-team.ru/maps/docker-baseimages/commit/cfee048) MAPSINFRA-3254: remove juggler (#225)
 * [e605f19](https://github.yandex-team.ru/maps/docker-baseimages/commit/e605f19) add req-id to logs in YT (#222)
 * [57896b8](https://github.yandex-team.ru/maps/docker-baseimages/commit/57896b8) MAPSINFRA-3230: fix cmd logs (#219)

## 2.2.1

 * [e654833](https://github.yandex-team.ru/maps/docker-baseimages/commit/e654833) MAPSINFRA-2966: Allow use custom DU name (#218)

## 2.2.0

 * [0ce9690](https://github.yandex-team.ru/maps/docker-baseimages/commit/0ce9690) MAPSINFRA-2629: user ip/port to logs (#217)

## 2.1.0

 * [4e3c6ba](https://github.yandex-team.ru/maps/docker-baseimages/commit/4e3c6ba) MAPSINFRA-2777: Базовый образ для ubuntu:bionic (#214)

## 2.0.0

 * [396c899](https://github.yandex-team.ru/maps/docker-baseimages/commit/396c899) MAPSINFRA-1486: Обновить nginx в боевом базовом образе (#216)
 * [02d50e6](https://github.yandex-team.ru/maps/docker-baseimages/commit/02d50e6) MAPSINFRA-2778: Обновить рокфор (#215)

## 1.0.1

 * [cc189d6](https://github.yandex-team.ru/maps/docker-baseimages/commit/cc189d6) MAPSINFRA-2728: NODE_EXTRA_CA_CERTS не доступен во время docker build (#213)

## 1.0.0

 * [112bdeb](https://github.yandex-team.ru/maps/docker-baseimages/commit/112bdeb) use close instead of exit to fully read stdout; (#210)
 * [4f32a5e](https://github.yandex-team.ru/maps/docker-baseimages/commit/4f32a5e) MAPSINFRA-2295: reduce nginx worker to 2 (#209)
 * [3003f48](https://github.yandex-team.ru/maps/docker-baseimages/commit/3003f48) FIX: return MAPS_DEPLOY_UNIT for Qloud platform
 * [5cc6302](https://github.yandex-team.ru/maps/docker-baseimages/commit/5cc6302) MAPSINFRA-2244: portoclt & ssl/ca (#208)
 * [bac8fef](https://github.yandex-team.ru/maps/docker-baseimages/commit/bac8fef) add nee dev-domain
 * [c835abb](https://github.yandex-team.ru/maps/docker-baseimages/commit/c835abb) MAPSINFRA-2194: add *.deneb.maps.dev.yandex.TLD to local crt (#207)
 * [3a79d43](https://github.yandex-team.ru/maps/docker-baseimages/commit/3a79d43) [Deploy] Fixed MAPS_LOGBROKER_TOPIC
 * [885587a](https://github.yandex-team.ru/maps/docker-baseimages/commit/885587a) MAPSINFRA-2093: fixed `hard` argument
 * [d7c1214](https://github.yandex-team.ru/maps/docker-baseimages/commit/d7c1214) MAPSINFRA-2093: [Deploy] Graceful degradation
 * [f6b3bfe](https://github.yandex-team.ru/maps/docker-baseimages/commit/f6b3bfe) Update motd
 * [2a8cdf6](https://github.yandex-team.ru/maps/docker-baseimages/commit/2a8cdf6) Update start.sh
 * [dfaab63](https://github.yandex-team.ru/maps/docker-baseimages/commit/dfaab63) Update accesslog-tskv.template.conf
 * [508f30c](https://github.yandex-team.ru/maps/docker-baseimages/commit/508f30c) fix start.sh
 * [842fa17](https://github.yandex-team.ru/maps/docker-baseimages/commit/842fa17) fix roquefort-custom supervisor.conf
 * [67892b4](https://github.yandex-team.ru/maps/docker-baseimages/commit/67892b4) Update accesslog-tskv.template.conf
 * [6e85527](https://github.yandex-team.ru/maps/docker-baseimages/commit/6e85527) Update common-env-values.sh
 * [59641db](https://github.yandex-team.ru/maps/docker-baseimages/commit/59641db) fix start.sh
 * [38e8428](https://github.yandex-team.ru/maps/docker-baseimages/commit/38e8428) MAPSINFRA-1986: Unified baseimage (#203)
 * [c3e49a3](https://github.yandex-team.ru/maps/docker-baseimages/commit/c3e49a3) MAPSINFRA-1476: turn off proxy_intercept_errors (#204)
 * [6ed7325](https://github.yandex-team.ru/maps/docker-baseimages/commit/6ed7325) MAPSINFRA-1981: [base-image] Убрать ограничение с ручки /close
 * [ee2a9a7](https://github.yandex-team.ru/maps/docker-baseimages/commit/ee2a9a7) MAPSINFRA-1847: Добавить jq в базовый образ
 * [5e1560e](https://github.yandex-team.ru/maps/docker-baseimages/commit/5e1560e) MAPSINFRA-1914: Update prepare-roquefort.js
 * [6a3dc0f](https://github.yandex-team.ru/maps/docker-baseimages/commit/6a3dc0f) Pass original "host" header if possible (#197)
 * [b269d91](https://github.yandex-team.ru/maps/docker-baseimages/commit/b269d91) fix DEV mode
 * [18a2a3a](https://github.yandex-team.ru/maps/docker-baseimages/commit/18a2a3a) MAPSINFRA-1082: add dev-https to baseimage (#195)
 * [e030a6f](https://github.yandex-team.ru/maps/docker-baseimages/commit/e030a6f) Не использовать дефолтный лог для кастомного рокфора
 * [988ff3d](https://github.yandex-team.ru/maps/docker-baseimages/commit/988ff3d) Turning off services by deleting symlinks (#194)
 * [2f745f7](https://github.yandex-team.ru/maps/docker-baseimages/commit/2f745f7) MAPSINFRA-1485: Причесать документацию в docker-baseimages
 * [6a549b9](https://github.yandex-team.ru/maps/docker-baseimages/commit/6a549b9) Fix app boot (#192)
 * [92caa4e](https://github.yandex-team.ru/maps/docker-baseimages/commit/92caa4e) MAPSINFRA-1488: Убить vanilla базовый образ


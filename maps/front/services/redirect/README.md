# Redirect

Проект для редиретка старых доменов

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-redirect |
| Qloud | https://platform.yandex-team.ru/projects/maps/front-redirect |

## Documentation

Проект живет в Qloud-е, за L3 балансерами (L3 над компонентой). Для работы используются внешние сертификаты. Доставляются через секретницу Qloud-a.

## SSL сертификаты
Все сертификаты нужные для работы заказываются через [Сертификатницу](https://crt.yandex-team.ru/certificates). Все сертификаты
заказываются на проект [maps-front-redirect](https://abc.yandex-team.ru/services/maps-front-redirect). [How-to](https://wiki.yandex-team.ru/maps/dev/ui/deploy/devops/#kakzakazatperevypustitsertifikat) по заказу сертификатов

## Known clients

Текущие проекты:

* metro.yandex.tld
* navigator.maps.yandex.ru
* probki.yandex.tld
* maps.yandex.tld
* constructor.maps.yandex.tld
* old.maps.yandex.tld
* maps.wiki.yandex.ru
* maps.ya.ru
* old.n.maps.yandex.ru

## What happens when service is down

* Не будет работать переадресация со старых доменов, таких как
    * maps.ya.ru -> yandex.ru/maps
    * metro.yandex.ru -> yandex.ru/metro
    * и т.д.

### production

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/?query=host%3Dqloud-ext.maps.front-redirect.production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front/full_env_name=maps.front-redirect.production/ |

## Logs
| Name | URL |
|---|---|
| Platform | https://platform.yandex-team.ru/projects/maps/front-redirect/production?tab=logs |
| YT | `hahn.[home/logfeller/logs/maps-log/1d/2019-05-15]`, [example in YQL](https://yql.yandex-team.ru/Operations/XN0__QlSst0zUHtNvPwHSNl6aVHrEg8chdXk3v6cpl4=) |

# Как обновить node.js

**ВАЖНО:** мы не используем пакетов с нодой из внешнего интернета,
потому что у нас есть необходимость иметь одновременно несколько версий ноды на продакшен-сервере.

Мы живем на LTS-версиях, если нет каких-то серьезных причин использовать другую версию.

yandex-сборка ноды ничем не отличается от ванильной за исключением путей.
Каждая мажорная версия в yandex-сборке ставится в отдельную папку `/opt/nodejs/<major_version>/...`.
Пакеты называются `nodejs-<major_version>`. Например, `nodejs-8`, `nodejs-10`.

## Регламент

1. Все наши сервисы выкатываются в docker, поэтому обновить nodejs надо только в дев-плейбуках, которые приезжают на виртуалку
   https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/frontend-dev/tasks/main.yml
После мержа в мастер, плейбуки выкатятся автоматически.
С свежей nodejs надо пожить пару дней, убедиться, что работают приложения и npm.
2. Обновить docker-образы с nodejs

## Сборка node.js

**Как узнать собрана ли нужная версия ноды?**

```
$ ssh duploader.yandex.ru

$ find_package nodejs-8
Searching in Cacus/MDS:

+----------------------+----------+----------------------------------------------------------------+
| repo                 | env      | package                                                        |
|----------------------+----------+----------------------------------------------------------------|
| yandex-xenial        | unstable | nodejs-8_8.11.3-1_amd64.deb                                    |
| yandex-xenial        | unstable | nodejs-8_8.11.4-1_amd64.deb                                    |
| yandex-xenial        | unstable | nodejs-8_8.12.0-1_amd64.deb                                    |
| yandex-vertis-xenial | unstable | nodejs-8_8.9.0-1_amd64.deb                                     |
| yandex-vertis-xenial | unstable | nodejs-8_8.11.1-1_amd64.deb                                    |
| yandex-vertis-xenial | unstable | nodejs-8_8.11.3-1_amd64.deb                                    |
| yandex-vertis-xenial | unstable | nodejs-8_8.12.0-1_amd64.deb                                    |
+----------------------+----------+----------------------------------------------------------------+
```

Мы используем пакеты ТОЛЬКО из реп `yandex-vertis-*`. Если нужный пакет есть в других репах, но нет у нас, то попросите админов или aandrosov@ скопировать пакеты в нужную репу.

**Как собрать новую версию?**

deb-пакет с nodejs собирается в [Teamcity](https://t.vertis.yandex-team.ru/buildConfiguration/vs_frontend_NodeJs_NodejsDebXenial64).
При сборке надо **ОБЯЗАТЕЛЬНО** указать какую версию надо собирать в формате `X.Y.Z`.
Ничего больше делать не надо, джоба скачает исходники ноды и соберет их в пакет.

После сборки deb-пакета надо собрать:
1. новый образ только с nodejs https://a.yandex-team.ru/arcadia/classifieds/infra/admin-dockerfiles/nodejs-focal
2. новый образ с nodejs+биндинги https://a.yandex-team.ru/arcadia/classifieds/infra/admin-dockerfiles/frontend-nodejs-14-focal

**Что делать, если с новой версией не работают биндинги в geobase/uatraits**

Биндинги переписаны на n-api и не должны ломаться.
Если что-то случится, то надо идти к коммитерам аркадии и спрашивать их.
* [@yandex-int/geo](https://a.yandex-team.ru/arc/trunk/arcadia/serp/geobase/ts)
* [@yandex-int/uatraits](https://a.yandex-team.ru/arc/trunk/arcadia/mail/nodejs/js/uatraits)

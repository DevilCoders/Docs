Что это?
========

dcsaap - DCS as a platform.

Продолжение сверок:

  - https://wiki.yandex-team.ru/check/

Концепция новой версии:

  - https://wiki.yandex-team.ru/check/Development/concept-2.0/

**Table of Contents:**

* [Что это?](#что-это)
* [Разработка](#разработка)
* [Где посмотреть?](#где-посмотреть)
  * [Dev](#dev)
  * [Test](#test)
  * [Prod](#prod)
* [Квоты](#квоты)
* [Deploy](#deploy)
  * [Проект](#проект)
  * [Доступы](#доступы)
  * [Логи](#логи)
* [Сборка релиза](#сборка-релиза)
  * [Новый релиз](#новый-релиз)
  * [Новая версия](#новая-версия)
  * [Конфликты](#конфликты)
* [Выкладка релиза](#выкладка-релиза)
  * [Dev, Test](#dev-test)
  * [Prod](#prod-1)
* [Миграции](#миграции)
* [Локальный запуск](#локальный-запуск)
* [Локальный запуск в docker](#локальный-запуск-в-docker)
  * [Подготовка](#подготовка)
  * [Сборка и запуск](#сборка-и-запуск)
* [Сборка docker образа](#сборка-docker-образа)
* [Используемые переменные окружения](#используемые-переменные-окружения)
* [Используемые роботы](#используемые-роботы)
* [Nirvana](#nirvana)
  * [Роли](#роли)
  * [Квота](#квота)
  * [Наши операции](#наши-операции)
* [UI](#ui)
* [Мониторинги](#мониторинги)
* [Отключение трафика](#отключение-трафика)
* [Доступ к бд](#доступ-к-бд)
* [Настройки SQS](#настройки-sqs)
* [Работа в QYP](#работа-в-qyp)

Разработка
==========

Для проекта включены тесты на соблюдение [Arcadia Python Style Guide](https://docs.yandex-team.ru/arcadia-python/python_style_guide).
Для упрощения внесения изменений можно настроить автоматическое применение `ya style` при использовании PyCharm: [инструкция](https://wiki.yandex-team.ru/balance/fintools/pycharm-ya-style/).

Где посмотреть?
===============

Dev
---

- UI: https://dcs-dev.yandex-team.ru/
- API: https://dcs-dev.yandex-team.ru/api/v1
- IDM: https://idm.test.yandex-team.ru/system/dcsaap
- ErrorBooster: https://error.yandex-team.ru/projects/dcsaap/projectDashboard
- Логи: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/paysys-balance-dcs-development-balance-dcs

Test
----

- UI: https://dcs-test.yandex-team.ru/
- API: https://dcs-test.yandex-team.ru/api/v1
- IDM: https://idm.test.yandex-team.ru/system/dcsaap-testing
- ErrorBooster: https://error.yandex-team.ru/projects/dcsaap/projectDashboard
- Логи: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/paysys-balance-dcs-testing-balance-dcs
- Балансер (общий): https://qloud-ext.yandex-team.ru/projects/paysys/slb/paysys-int-test?tab=dashboard

Prod
----

- UI: https://dcs.yandex-team.ru/
- API: https://dcs.yandex-team.ru/api/v1
- IDM: https://idm.yandex-team.ru/system/dcsaap
- ErrorBooster: https://error.yandex-team.ru/projects/dcsaap/projectDashboard
- Логи: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/paysys-balance-dcs-production-balance-dcs
- Балансер (личный): https://qloud-ext.yandex-team.ru/l7/balance-dcs?tab=dashboard
- Графана (БД): https://grafana.yandex-team.ru/d/K-ZibbUWz/cluster-list?orgId=1&var-cluster_id=mdbe1pf6lkuo4a3n70tm
- Мониторинги (MDB): https://yc.yandex-team.ru/folders/foo6phbgfabvu8142do1/managed-postgresql/cluster/mdbe1pf6lkuo4a3n70tm?section=monitoring


Квоты
=====

- Nirvana: https://dispenser.yandex-team.ru/nirvana/projects/dcsaap
- БД: https://dispenser.yandex-team.ru/db/projects/check

Deploy
=====

Проект
------

- https://deploy.yandex-team.ru/projects/billing-dcs

Доступы
-------

Исходящие (мы - источник):
- Дев, тест: `_BILLING_DEPLOY_DCS_TEST_NETS_`
- Прод: `_BILLING_DEPLOY_DCS_PROD_NETS_`

Входящие (мы - назначение):
- Дев: `dcs-dev.yandex-team.ru`
- Тест: `dcs-test.yandex-team.ru`
- Прод: `dcs.yandex-team.ru`

Логи
-----

**В продакшене**:

Для упрощения поиска в продакшен логах можно использовать функции для работы с JSON:
- в CHYT:
```yql
USE chyt.hahn;

SELECT
    JSONExtractString("data", 'message') as message,
    "data"
FROM "//home/logfeller/logs/paysys-balance-dcs-development-balance-dcs/stream/5min/2021-03-25T14:40:00"
WHERE JSONExtractUInt("data", 'process') = 351
    AND JSONExtractUInt("data", 'thread') = 140355908012672;
```

- в YQL:
```yql
use hahn;

SELECT
    json_value(cast(`data` as json), '$.message' returning utf8) as message,
    `data`
FROM `//home/logfeller/logs/paysys-balance-dcs-development-balance-dcs/stream/5min/2021-03-25T14:40:00`
WHERE json_value(cast(`data` as json), '$.process' returning uint64) = 351
    AND json_value(cast(`data` as json), '$.thread' returning uint64) = 140355908012672;
```

**В приложении**:

В Deploy получаем строку подключения для нужного deploy unit (`app`/`celery`) в нужном датацентре (`SAS`/`VLA`) (выпадающий список в таблице `FQDN`, `Host`, ...).

Далее:

```
$ ssh root@billing-dcs-app.3e5navxtovx3b4sr.sas.yp-c.yandex.net
root@sas1-4592-2.3e5navxtovx3b4sr.sas.yp-c / # less /var/log/supervisor/app.log
```

Сборка релиза
=============

Arcadia CI:

- https://a.yandex-team.ru/projects/check/ci/releases/timeline?dir=billing%2Fdcsaap&id=dcsaap-release

Собираются docker образы:
 - для `dcsaap` пушится в `registry.yandex.net/billing/dcsaap:*`
 - для `dcsaap-celery` пушится в `registry.yandex.net/billing/dcsaap-celery:*`

Конфигурация:

- https://a.yandex-team.ru/arc_vcs/billing/dcsaap/a.yaml

Подключали в тикете:

- https://st.yandex-team.ru/CHECK-3472

Новый релиз
-----------

Из `trunk` нажимаем `Run Release`, отколется новая релизная ветка из `trunk` и запустится сборка docker-образов.

Новая версия
------------

Идём на страницу:

- https://a.yandex-team.ru/projects/check/ci/releases/timeline?dir=billing%2Fdcsaap&id=dcsaap-release

Выбираем ветку, в которую планируем влить изменения и копируем её название (например `releases/dcsaap/16`).
Идем в развернутый локально `arc` и выполняем:
```bash
# Подтягиваем выбранную релизную ветку
$ arc fetch releases/dcsaap/15
# Переключаемся на неё
$ arc checkout releases/dcsaap/15
# Подтягиваем нужный коммит (здесь можно указать несколько коммитов через пробел)
$ arc cherry-pick r123456
# Пушим в релизную ветку
$ arc push
```

Возвращаемся в интерфейс, проверяем что выбрана нужная ветка и нажимаем `Run release`.
Запустится сборка docker-образов с новой версией.

Конфликты
---------

Иногда указанная версия не может быть влита в ветку без изменений.
В этом случае `arc` выдаст ошибку и скажет, что есть конфликты:
```
$ arc cherry-pick 703e320485d5d9e533a748d5e9f02bba2e173067
nothing to commit, working directory clean
commit 703e320485d5d9e533a748d5e9f02bba2e173067  Example
there are some conflicts:
    content  billing/dcsaap/README.md  cf8bf89cdc6aaf55e634a3a30249d0f6a4d6ec6a
cherry-pick wasn't performed.
  (use "arc show <blobid>" to see conflicted lines)
```

Решается как и обычный конфликт, например через Pycharm: меню `VCS - Arc - Resolve Conflicts...`.

После решения конфликта:
```bash
$ arc add billing/dcsaap/README.md
$ arc cherry-pick --continue
$ arc push
```

Выкладка релиза
===============

Dev
---

После окончания шага сборки в CI заходим в Deploy:
- https://deploy.yandex-team.ru/stages/billing-dcs-dev-stage

Нажимаем `Edit` и переходим в `billing-dcs-app` (box).
Находим группу настроек `Base layer` и напротив `https://registry.yandex.net/` прописываем собранную версию
(версии не подставляются автоматически, поэтому берем версию из [интерфейса CI](https://a.yandex-team.ru/projects/check/ci/releases/timeline?dir=billing%2Fdcsaap&id=dcsaap-release)).

Аналогично прописываем версию в `billing-dcs-celery`. Жмем `Update`.

В `dev` окружении можно выбрать любой образ для выкладки. Поэтому, чтобы не ждать (иногда)
долгой сборки в CI или для простой проверки гипотезы без комита в `trunk` можно собрать свой
образ и проверить его в `dev`:

```bash
# создаем новую ветку из trunk
$ arc checkout -b CHECK-3270/fix-user-detection-for-tvm

# собираем образ для своего пользователя (проверяем, что собирается)
$ make build-docker-dev-image [build-docker-dev-image-celery]

# собираем и публикуем образ в docker registry
$ make release-dev [release-dev-celery]
```

В результате, в реестре появится образ `<YA_USER|USER>/dcsapp:<ветка-из-которой-собиралось>`.
Его можно спокойно использовать в Deploy. Вы так же автоматически станете владельцем
`registry.yandex.net/<YA_USER|USER>`.

Где:
- `$YA_USER` - переменная окружения для настройки `ya/arc/etc`. Особенно нужна, если имя
пользователя в OS не совпадает с логином в yandex-team.ru.
- `$USER` - имя пользователя в OS.

При попытке первый раз выкатить свой образ в dev, Deploy "скажет", что у него нет прав на указанный
образ:

```
Resolving docker image DockerImageDescription{registryHost=registry.yandex.net, name=srg91/dcsaap, tag=users/srg91/CHECK-1234, digest=}
```

Чтобы доступ появился, в IDM выдаем доступ роботу robot-qloud-client@ на наш префикс:
- https://idm.yandex-team.ru/#rf-role=yfAtFM7X#user:robot-qloud-client@docker/distribution_prefix(fields:();params:()),rf-expanded=yfAtFM7X,rf=1

Т.к. вы сами являетесь владельнем этого образа, то права в IDM будут выданы тут же.

Test
----

Для выкладки в тест нужно "сказать" релизу, что можно выкладываться. Для этого нужно:
- зайти в CI: https://a.yandex-team.ru/projects/check/ci/releases/timeline?dir=billing%2Fdcsaap&id=dcsaap-release
- выбрать нужную ветку
- выбрать нужный релиз (нажать на `Release DCSaaP #16.2`)
- на первом кубике в стадии `Testing` нажать кнопку `Play`

Это запустит автоматическу выкладку этого релиза на тест.

Prod
----

После того, как релиз был выложен на тест - его можно покатить в прод.
Для этого нужно:
- зайти в CI: https://a.yandex-team.ru/projects/check/ci/releases/timeline?dir=billing%2Fdcsaap&id=dcsaap-release
- выбрать нужную ветку
- выбрать нужный релиз (нажать на `Release DCSaaP #16.2`)
- на первом кубике в стадии `Production` нажать кнопку `Play`

CI создаст релизный тикет со всеми изменениями, вошедшими в в релиз.
Менеджер должен подтвердить этот тикет и перевести его в статус `Подтверждён`.
После этого запустится процесс выкладки docker-образов на прод.

Для попадания проекта в Tier C была включена полокационная выкладка в Deploy.
После начала выкладки нужно зайти в [stage](https://deploy.yandex-team.ru/stages/billing-dcs-prod-stage/)
 и подтвердить выкладку в каждый из ДЦ.
После успешной раскатки в этом ДЦ проверяем, что всё работает и подтвержаем выкладку в следующий ДЦ.

Например:
- https://st.yandex-team.ru/CHECK-3508

Автоматизация была выполнена в рамках тикета:
- https://st.yandex-team.ru/CHECK-3472

Миграции
========

Для БД миграций используется механизм, идущий в составе Django.
Все миграции накатываются перед стартом приложения:

- https://a.yandex-team.ru/arc/trunk/arcadia/billing/dcsaap/docker/run.sh?rev=5889878#L4

Запрос для просмотра выполненных миграций в БД:

```sql
> select * from django_migrations order by applied desc;
```

Локальный запуск
================

Api server
----------

В отдельном терминале:

```sh
$ make dev-backend
```

Добавление пользователя
-----------------------

Миграции
```sh
$ cd backend && make dev-migrate; cd -
```

Добавляем пользователя в БД:

```sh
$ cd backend && SOLOMON_TOKEN="xxxx" ./manage/manage \
    createsuperuser --username ${USER} --noinput  --email "${USER}@yandex-team.ru"; \
    cd -
```

Сертификаты
-----------

Устанавливаем `mkcert` и запускаем, чтобы установить центр-сертификации в Chrome и Firefox:

```sh
cd certs && make deps; cd -
```

Установка через `make deps` работает только для `Linux`, для остальных систем нужно сделать руками (см. `certs/Makefile`).

### Chrome

Должно заработать сразу.

### Firefox

Возможно потребуется дополнительно прописать исключения для локального сервера:
- Запускаем Firefox, открываем `Меню - Settings`;
- Заходим в `Privacy & Security > Certificates > View Certificates`, вкладка `Servers`;
- Нажимаем `Add Exception`, в `Location` прописываем `https://dcs-local.yandex-team.ru:3000`, нажимем `Get Certificate`.

Настройка домена
----------------

Добавляем `dcs-local.yandex-team.ru` как `127.0.2.1`:

```sh
$ make dev-domain
```

UI dev server
-------------

```sh
$ make dev-ui-ssl
```

После этого, дожен заработать:

- https://dcs-local.yandex-team.ru:3000/

Локальный запуск в docker
=========================

Подготовка
----------

Docker образ основан на образе `paysys/balance-dcs`, который нам подготовили
[админы](https://staff.yandex-team.ru/departments/yandex_mnt_fin_payment)
(а точнее: [fedusia@](https://staff.yandex-team.ru/fedusia)). Поэтому перед тем,
как собрать образ локально и запустить, необходимо:

- получить право `viewer` в для `Docker-registry / Префиксы / paysys`
- настроить локально [docker авторизацию](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)

Сборка и запуск
---------------

```bash
$ make run-container
```

Соберет все нужные бинарники, соберет docker image
(`registry.yandex.net/billing/dcsaap`) и запустит контейнер на его основе.

Далее смотрим, что поднялось:

```bash
$ ➜ curl http://127.0.0.1:8080/api/v1/
{"users":"http://127.0.0.1:8080/api/v1/users/","groups":"http://127.0.0.1:8080/api/v1/groups/"}
```

Сборка docker образа
====================

```bash
$ make docker-image

$ docker images | grep billing
registry.yandex.net/billing/dcsaap        latest              816bac465199
7 minutes ago       1.43GB
```

Используемые переменные окружения
=================================

Для работы с Nirvana (запуск приложений):

- `NIRVANA_API_TOKEN` - токен для запуска nirvana flow
- `NIRVANA_DEFAULT_WORKFLOW_ID` - дефолтный workflow_id
- `NIRVANA_DEFAULT_INSTANCE_ID` - дефолтный instance_id в указанном workflow_id

Для работы с YT (чтение расхождений с YT):

- `YT_API_TOKEN` - токен для работы с YT

Для работы с PG (MDB):

- `PAYSYS_PG_DB_HOST` - хост
- `PAYSYS_PG_DB_PORT` - порт
- `PAYSYS_PG_DB_USER` - пользователь
- `PAYSYS_PG_DB_PASS` - пароль
- `PAYSYS_PG_DB_NAME` - имя бд (обычно совпадает с именем пользователя)

Для работы с TVM (ограничение доступа к API):

- `TVM2_CLIENT_ID` - ID приложения, из-под которого работаем
- `TVM2_ALLOWED_CLIENT_IDS` - ID приложения, которым разрешено ходить к нам (включая самого себя)
- `TVM2_SECRET` - секрет (пока не нужен, понадобится, если мы будем ходить в другие сервисы)

Дополнительно:

- `DEPLOY_ENVIRONMENT` - тип окружения в Deploy, для тестов и локальной разработки не заполнен

Используемые роботы
===================

- https://staff.yandex-team.ru/robot-checkbot (прод)
- https://staff.yandex-team.ru/robot-checkbot-test (тест, дев)
- https://staff.yandex-team.ru/robot-checkbot-ci (CI)

Nirvana
=======

## Роли

- https://nirvana.yandex-team.ru/roles/nirvana.dcsaap
- https://nirvana.yandex-team.ru/roles/nirvana.flowchart.dcs-aap
- https://nirvana.yandex-team.ru/roles/nirvana.operation.dcs-aap

## Квота

[Система сравнения данных](https://dispenser.yandex-team.ru/nirvana/projects/dcsaap)

В данный момент квота для запуска устанавливается в настройках конкретного инстанса в Nirvana.

В созданном для запуса черновике открывается меню [Instance Details](https://jing.yandex-team.ru/files/srg91/Screenshot%202020-03-19%20at%2014.12.59.png) (хоткей `Alt+3`), после чего во вкладке `Config` из выпадающего списка `Quota` выбирается квота [Система сравнения данных](https://jing.yandex-team.ru/files/srg91/Screenshot%202020-03-19%20at%2014.15.52.png).

## Наши операции

* [Сверка с отчётом об окончании](https://nirvana.yandex-team.ru/operation-old/1d8fdd12-8e40-4c0e-a4ba-5f1799070e50/overview)
* [Отчёт об окончании](https://nirvana.yandex-team.ru/operation-old/eb8f9392-7d06-4f84-8f39-e1036624374e/overview)
* [YQL с переключением при неудаче](https://nirvana.yandex-team.ru/operation-old/d843bf00-f539-496c-98fa-4aa9012ef1ca/overview)
* [До 4 текстовых входов в 1 json](https://nirvana.yandex-team.ru/operation/033e64eb-fda5-44b2-a466-86316b5a037f)

## Сеть

Сетевой макрос, откуда идут обращения к нашей системе в процессе работы операций:

- `_NIRVANA_REGULAR_JOB_NETS_`

UI
==

UI построен на базе [react-admin](https://github.com/marmelab/react-admin). В силу особенностей
работы Аркадии, в ней хранится не только исходный код, но и сборка. То есть, после того, как выполнена
какая-либо доработка, надо сделать:

```shell script
$ make frontend-build
$ arc add frontend/build
```

Только после этого изменение появится в docker-образе.

Используется тот же образ, что и для backend'a. Отдается как статика через uwsgi.

Зарезервированные URL пути:

- `/s` - статика django приложения (настроено в `uwsgi.ini`)
- `/static` - статика react приложения (`uwsgi.ini`)
- `/ui` - точка запуска для react приложения (`uwsgi.ini`)
- `/` - перенаправляет на `/ui` (происходит в backend'e)

Мониторинги
===========

## Monitoring-as-a-Code

В связи с переездом в Deploy в наше распоряжение так же перехали и мониторинги.
Большинство мониторингов настраивается с помощью [проекта в Monitoring-as-a-Code](../../paysys/sre/tools/monitorings/configs/dcsaap).

Чтобы раскатить новые мониторинги нужно выполнить:

```sh
$ cd ../../paysys/sre/tools/monitorings
$ make build
$ make run -- --project dcsaap --environment stable -v
```

Увидеть созданные мониторинги можно в [Juggler](https://juggler.yandex-team.ru):
- тест: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Ddcsaap.testing
- прод: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Ddcsaap.production

## Solomon

| Среда | Ссылка |
| ------|--------|
| Дев   | https://solomon-prestable.yandex-team.ru/?project=dcsaap&cluster=dev&service=dcsaap-pull&graph=auto |
| Тест  | https://solomon-prestable.yandex-team.ru/?project=dcsaap&cluster=test&service=dcsaap-pull&graph=auto |
| Прод  | https://solomon.yandex-team.ru/?project=dcsaap&cluster=prod&service=pull&graph=auto&b=1d&e= |


## ErrorBooster & Jugler

В ErrorBooster настроены алерты по кол-ву ошибок:

- https://error.yandex-team.ru/projects/dcsaap/settings/alerts

Они подхватываются в Juggler:

- https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5fffee5ed4e462e087df6ab4

Отправляются в чатик в Telegram.

Отключение трафика
==================

Во время учений или технических работ может потребоваться отключить трафик в одном из датацентров.
Для этого используется [L7-heavy](https://nanny.yandex-team.ru/ui/#/list-l7heavy/) в Nanny.

Для отключения трафика:
- Находим нужный нам L3-балансер, в зависимости от среды (ссылки преведены ниже) и проваливаемся в него
- Выбираем датацентр, в котором требуется закрыть трафик (SAS, VLA или MAN)
- Нажимаем `Close w/ current weights`, что приведет к пересчету весов без учета выбранного датацентра
- Нажимаем `Save section weights` и `Push to ITS`

Для возвращения трафика:
- Аналогично отключению выбираем L3-балансер
- Под списком датацентров находим `Reset weights to defaults` и нажимаем, это приведет к возвращению весов в состояние по-умолчанию
- Нажимаем `Save section weights` и `Push to ITS`

Список наших L3-балансеров в ITS в зависимости от среды:
- `development`, датацентры SAS и VLA: https://nanny.yandex-team.ru/ui/#/l7heavy/dcs-dev-l7.paysys.yandex.net/
- `testing`, датацентры SAS и VLA: https://nanny.yandex-team.ru/ui/#/l7heavy/dcs-test-l7.paysys.yandex.net/
- `prodution`, датацентры SAS, VLA и MAN: https://nanny.yandex-team.ru/ui/#/l7heavy/dcs-prod-l7.paysys.yandex.net/

Доступ к бд
===========

Пароли для теста и дева тут:

- https://yav.yandex-team.ru/secret/sec-01dt1v7wdxkxzjtak5pe9rabpr

Postgresql кластеры тут:

- https://yc.yandex-team.ru/folders/foo6phbgfabvu8142do1/managed-postgresql

Заказать доступ можно тут:

- https://idm.yandex-team.ru/user/shorrty/roles#rf=1,rf-role=M2WbHIsp#user:shorrty@dbaas(fields:();params:()),f-status=all,sort-by=-updated,rf-expanded=M2WbHIsp

Кластера:

- balance_dcs
- balance_dcs_test

Подключение к БД:

```sh
# ${PG_USER} - balance_dcs_dev/balance_dcs_test/balance_dcs
# ${PG_HOST} - см. хосты в yc.yandex-team.ru
#                 - sas-usb28cf822kcr1jg.db.yandex.net (дев)
#                 - vla-0ftoihd1bhsjlv7d.db.yandex.net (тест)
# ${PG_PASS} - см. секрет
$ PGPASSWORD=${PG_PASS} psql "host=${PG_HOST} port=6432 sslmode=verify-full dbname=${PG_USER} user=${PG_USER} target_session_attrs=read-write"
```

Настройки SQS
============

Чтобы все заработало, надо дать доступ роботам в SQS:

```sh
$ aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions \
    --path dcs_aap-test \
    --subject robot-checkbot-test@staff \
    --permissions AlterQueue CreateQueue DeleteMessage DescribePath ReceiveMessage SendMessage

$ aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions \
    --path dcs_aap-dev \
    --subject robot-checkbot-test@staff \
    --permissions AlterQueue CreateQueue DeleteMessage DescribePath ReceiveMessage SendMessage

$ aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions \
    --path dcs_aap \
    --subject robot-checkbot@staff \
    --permissions AlterQueue CreateQueue DeleteMessage DescribePath ReceiveMessage SendMessage
```

Работа в QYP
============

Всем разработчикам Поискового портала доступны персональные виртуальные машины в [QYP](https://qyp.yandex-team.ru/). Такая виртуальная машина позволяет намного быстрее собирать проект и тестировать его (в сравнении с разработкой на ноутбуке).

Дополнительно для разработчиков Баланса выделен сетевой макрос `_BALANCE_QYP_VM_DEV_NETS_`, который позволяет запрашивать доступы до нужных Балансу систем. В данный момент из данного макроса есть доступ до `development` и `testing` сред проекта [balance-dcs](https://qloud-ext.yandex-team.ru/projects/paysys/balance-dcs). Если требуются дополнительные доступы, то они запрашиваются через [Puncher](https://puncher.yandex-team.ru) (источник `_BALANCE_QYP_VM_DEV_NETS_`).

Инструкция по созданию VM ([оригинал](https://wiki.yandex-team.ru/sandbox/allocate-host/#allocation)):
- Открываем [QYP](https://qyp.yandex-team.ru/)
- Нажимаем кнопку [Launch new VM](https://qyp.yandex-team.ru/create-vm)
- В поле `Network Macros` указываем `_BALANCE_QYP_VM_DEV_NETS_`
- В поле `Internet Access` включаем интернет
- Остальные поля можно заполняются по желанию в пределах разумного

В случае вопросов можно обратиться к [общей инструкции по QYP](https://wiki.yandex-team.ru/qyp/ui/).

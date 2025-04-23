# yb-ar
Yandex Balance Agency Rewards


## Содержание

   * [yb-ar](#yb-ar)
      * [Разработка](#разработка)
      * [Тестирование](#тестирование)
      * [Сборка](#сборка)
         * [Локальная сборка бинарников](#локальная-сборка-бинарников)
         * [Сборка deb пакетов](#сборка-deb-пакетов)
      * [Mount failed](#mount-failed)
      * [Как устроено версионирование / сборка пакетов](#как-устроено-версионирование--сборка-пакетов)
      * [Релизная политика](#релизная-политика)
      * [Выкладка](#выкладка)
         * [DDL в Дев](#ddl-в-дев)
         * [Тест](#тест)
         * [Прод](#прод)
      * [Запуск расчета](#запуск-расчета)
         * [Прод/Тест](#продтест)
         * [Локально](#локально)
            * [Окружение](#окружение)
            * [Запуск расчетов](#запуск-расчетов)
      * [Логи](#логи)
      * [Архитектура](#архитектура)
      * [Роботы](#роботы)


Просмотр активных расчетов платформы:

- https://st.yandex-team.ru/BALANCEAR/order:key:true/filter?resolution=empty()&status=confirmed

Бизнесовое описание платформы и как в ней работать:

- https://wiki.yandex-team.ru/Balance/AgencyRewardsPlatform/

Дашборд:
 - https://monitoring.yandex-team.ru/projects/balance-reports/dashboards/mon0l05ga8uic56551be?range=3mo&refresh=60

## Разработка

Для проекта включены тесты на соблюдение [Arcadia Python Style Guide](https://docs.yandex-team.ru/arcadia-python/python_style_guide).
Для упрощения внесения изменений можно настроить автоматическое применение `ya style` при использовании PyCharm: [инструкция](https://wiki.yandex-team.ru/balance/fintools/pycharm-ya-style/).

## Тестирование

Тесты можно запускать локально и на dev машинах.

- `make test` - запуск юнит тестов
- `make regress-platform-local` - запуск регрессионных тестов.

Перед запуском нужно прописать данные от БД, YT и YQL токены в локальный конфиг, `source /etc/oraprofile`.

Более подробно тут:

- [docs/testing](docs/testing.md)

## Сборка

### Локальная сборка бинарников

Только бинарники, не пакеты.

* `ya make` в корне проекта. После запуска появятся бинарники:
    - `agency_rewards/main/yb-ar-calculate-bin` - для запуска расчетов премий
    - `cashback/bin/yb-ar-cashback` - для запуска расчетов кэшбеков

### Сборка deb пакетов

#### Через RM/CI

Сначала необходимо отколоть новый тэг (новый релиз или новая версия уже существующего релиза) в релизной машине:

- https://rm.z.yandex-team.ru/component/agency_rewards

Если необходим новый релиз, жмем «Pre Release». Отколется новая релизная ветка из `trunk`.

Если необходима новая версия релиза, то переходим на страницу «Merge/Rollback»:

- https://rm.z.yandex-team.ru/component/agency_rewards/merge_rollback

В секции «Merge» указываем коммиты, которые будут добавлены в новую версию.
Далее, надо сходить в [CI](https://a.yandex-team.ru/projects/ybar/ci), в ветку,
которая была отколота, или в которую было влито новое изменение, и нажимаем `Run release`.

После этого `deb` пакеты соберутся автоматически и придёт отбивка в релизный тикет.

Проверить их наличие в репе можно так:

- http://dist.yandex.net/find?pkg=yb-ar&ver=2.21.2

#### Руками через SB

* `deb` - Нужно склонировать SB [задачу](https://sandbox.yandex-team.ru/task/525310028/view),
  проставить нужный тег в поле "Svn url for arcadia" (например, `arcadia:/arc/tags/agency_rewards/11.1/arcadia`,
  брать номер тэга из релизной машины [тут](https://a.yandex-team.ru/arc/tags/agency_rewards)) и запустить.
  Частичное описание [параметров](https://wiki.yandex-team.ru/users/mekagem/yapackage/#parametry)

После завершения выше указанных процедур пакеты загружаются в общеяндексовые репозитарии (deb: `yandex-trusty`).
Далее эти пакеты можно катить в прод/тест через кондуктор:

- [yb-ar](https://c.yandex-team.ru/packages/yb-ar) для python-кода
- [yb-ar-liquibase](https://c.yandex-team.ru/packages/yb-ar-liquibase) для ddl/миграций

## Mount failed

Если при сборке появляется ошибка:

```
ArcCommandFailed: Mount failed
```

Например:
- https://sandbox.yandex-team.ru/task/783410736/view

То, скорее всего, нужно обновить `ARC_TOKEN`:

- https://sandbox.yandex-team.ru/admin/vault?owner=YBAR


## Как устроено версионирование / сборка пакетов

Используется подход [семантического версионирования](https://semver.org/) для нумерации пакетов.

Для выкладки python-кода и DDL собираются deb-пакеты. Сами изменения в БД выкладываются
через [liquibase](https://www.liquibase.org).

Из аркадии собираются пакеты версии `2.*.*` (из GitHub собирались версии `1.*.*`).

Для откола веток мы используем [релизную машину](https://wiki.yandex-team.ru/ReleaseMachine/) (RM).
Информация об отколотых ветках можно найти [тут](https://rm.z.yandex-team.ru/component/agency_rewards).
По номеру ветки(X, в UI они выглядят как `agency_rewards/stable-X`) и тега(Y)
в RM, можно найти deb/rpm пакеты версии 2.X.Y.

Следующая версия в той же ветке - 2.X.(Y + 1), в новой ветке - 2.(X + 1).1

Конфиг релизной машины расположен тут:

- https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/release_machine/components/configs/agency_rewards.py

Если делаются какие-то изменения в RM, то чтобы они вступили в силу нужно дождаться
окончания сборок со сделанным коммитом тут:
- https://testenv.yandex-team.ru/?screen=job_history&database=testenv-trunk&job_name=BUILD_TEST_ENVIRONMENT_CORE_PACKAGE
- https://testenv.yandex-team.ru/?screen=job_history&database=sandbox-trunk&job_name=BUILD_SANDBOX_TASKS


## Релизная политика

- в RM лежат ветки, из которых можно катить в тест и в прод
- все изменения (PR) идут в `trunk`
- если какой-то PR нужен в релизной ветке, он мержится в ветку [тут](https://rm.z.yandex-team.ru/component/agency_rewards/merge_rollback)

## Выкладка

### DDL в Дев

Подготовить окружение и конфиг (нужно сделать один раз):

```sh
$ make dev-ddl-env
$ make dev-ddl-conf
```

Далее выкладка миграций:

```sh
$ make dev-ddl
```

Если вдруг выкладка сломалась где-то в середине и блокировка не снялась с
таблицы миграций, то можно снять блокировку руками:

```sh
$ make dev-ddl-unlock
```

Все примененный миграции можно посмотреть так:

```sql
meta> select * from bo.ar_databasechangelog order by dateexecuted desc;
```

### Тест

- Создать тикет в кондукторе (testing). И он сам раскатится

### Прод

- Создать тикет к кондукторе (stable)
- В релизный тикет, который создает RM, вписать его
- Подтвердить релизный тикет (статус == Подтверждён)
- Запустить выкладку отсюда:
  - https://timeline.paysys.yandex-team.ru/pipe/projects/deploy/release/new/deploy-start-release-agency-rewards

## Запуск расчета

### Прод/Тест

Весь процесс расчета запускается по расписанию через [pycron](https://wiki.yandex-team.ru/balance/docs/process/pycron/).

Описание мастера (бд баланса):

```sql
select * from bo.v_pycron where name = 'yb-ar rewards master';
```

Все компоненты:

```sql
select * from bo.v_pycron where name like 'yb-ar%';
```

- `yb-ar client testing` - тестирование расчета на данных автора расчета
- `yb-ar forecast` - прогнозирование
- `yb-ar monitoring` - мониторинг (состояние основных MV)
- `yb-ar node creation` - создание узлов в Бункере и запрос прав в IDM для новых расчетов
- `yb-ar rewards master` - расчет
- `yb-ar-check-reward-errors` - проверка ошибок в расчете
- `yb-ar-import-*` - импорты данных

### Локально

#### Окружение

Для начала необходимо установить [ya](https://wiki.yandex-team.ru/arcadia/starterguide/).
Далее счекаутить проект:

```bash
$ mkdir -p arc && cd arc
$ mkdir -p arcadia store
$ arc mount -m arcadia/ -S store/
```

Далее сборка:

```bash
$ cd arcadia/billing/agency_rewards
$ ya make
```

Теперь у нас есть бинарник, который можно запускать.

#### Запуск расчетов

```
$ YANDEX_XML_CONFIG=./deployment/configs/calculate.cfg.local.xml \
    agency_rewards/main/yb-ar-calculate-bin [--no-mnclose --no-dt-checks --no-mv-refresh --no-plsql-calc]
```

## Логи

Все логи с прод машин смонтированы на машине `greed-dev2h.paysys.yandex.net`.

Просмотр списка логов за сегодня:

```bash
$ ls -l /var/remote-log/greed*/yb/agency_rewards*
```

Архивные логи (за вчера и позже):

```bash
$ ls -l /var/remote-log/archive/balance-back/stable/greed*/log/yb/arc/agency_rewards.*
```


## Архитектура

- [1.0](docs/arch-plsql.md)
- [2.0](docs/arch-python.md)
- [3.0](docs/arch-platform.md)

## Роботы

- Прод:
  - https://staff.yandex-team.ru/robot-balance-ar
  - Пароль у админов
- Тест:
  - https://staff.yandex-team.ru/robot-balance-ar-tst
  - Секреты:
    - https://yav.yandex-team.ru/secret/sec-01de4fpr2m9nk7rh6tp79zfysq
    - https://yav.yandex-team.ru/secret/sec-01ddtc0rpvm9qjrjn5gvv38p28

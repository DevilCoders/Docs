## Тестирование

Для тестирования достаточно прочитать [доку](https://wiki.yandex-team.ru/yatool/test/)

### Юнит тесты

Тесты, которым не нужны никакие внешние системы (БД, YT и прочее).

```bash
$ make test
```

### Интеграционные тесты (платформа)

Основные интеграционные тесты тут:

```bash
# запуск на ноутбуке разработчика
$ make regress-platform-local

# запуск на тестовом сервере
$ make regress-platform
```

### Как устроены интеграционные тесты

Цель интеграционных тестов - полностью повторить работу всего кода "как в продакшене".
Во время интеграционных тестов изменяется только:

- место забора исходных данных. Маппинг таблиц можно посмотреть в классе `ARData` (файл: `agency_rewards/common/__init__.py`).
- отключаются:
  - нотификации (`--no-notifications`)
  - проверка графа закрытия (`--no-mnclose`)
  - проверка сроков работы конкретного расчета (`--no-dt-checks`)
  - выгрузки агрегатов в YT (`--no-acts-yt-upload`), каждый тест сам пишет свои тестовые данные (см. далее)
  - обновление MV (`--no-mv-refresh`)
  - отключаются старые PLSQL расчеты (`--no-plsql-calc`), т.к. они давно не меняются, долго работают и тестами не покрыты

Тесты состоят из 3х этапов:

- генерация тестовых данных (метод `setup_fixtures` в каждом TestCase из модуля `tests_regression`)
- запуск расчета (с ключём `--regression-tests`)
- запуск тестов (из модуля `tests_regression`)

Описания расчетов для регрессионных тестов находятся тут:

- [deployment/bunker/regression](https://a.yandex-team.ru/arc/trunk/arcadia/billing/agency_rewards/deployment/bunker/regression)

Они так же продублированы в Бункере (именно оттуда они берутся, когда запускаются тесты):

- [agency-rewards/dev/regression](https://bunker.yandex-team.ru/agency-rewards/dev/regression)

В Бункере можно не публиковать расчеты, достаточно только сохранить.

Код, отвещающий за генерацию тестовых данных находится тут:

- [tests_platform/generators](https://a.yandex-team.ru/arc/trunk/arcadia/billing/agency_rewards/tests_platform/generators)

Сами тесты находятся в одноименных файлах уровнем выше. Ранее (до Аркадии) тесты и данные для них
были в одном модуле. Их разнесли из-за особенностей Аркадии:
  - тесты должны быть описаны в `PY3TEST`, и из них нельзя импортировать. Поэтому этот код нельзя использовать в
    программе генерации данных, которая выполняется отдльно от тестов
  - чтобы что-то можно было импортировать, оно должно быть описано в `PY3_LIBRARY`
  - генератор данных должен быть программой (`PY3_PROGRAM`)

#### Запуск контейнера с БД для регресионных тестов

Тесты могут быть запущены на пустой БД. То есть, можно поднять docker контейнер с Oracle БД
и прогнать на нем тесты:

* Установить docker и sqlplus
* Собрать нужную версию базы [по инструкции](https://github.com/oracle/docker-images/tree/master/OracleDatabase/SingleInstance)
* Добавить в tnsnames.ora:
```
testdb = (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=localhost)(PORT=1521))
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=orcl)
      )
)
```
* Запустить один раз ```make run_db_container```
* Запускать тесты

Если контейнер неактивен, нужно запустить ```make run_db_container```.
Для изменения объектов в базе нужно изменить init.sql и перезапустить контейнер.

#### Запуск интеграционных тестов на testing сервере

Будет использоваться тестовая БД, все пароли будут браться из стандартных мест (`/etc/...``).

Чтобы запустить тесты, необходимо получить исходный код:

```bash
# Настраиваем arc
shorrty@greed-ts1h.paysys ~ $ export ARC_TOKEN='AQAD-...'
shorrty@greed-ts1h.paysys ~ $ mkdir -p ~/.arc ; chmod 700 ~/.arc
shorrty@greed-ts1h.paysys ~ $ echo -n $ARC_TOKEN > ~/.arc/token ; chmod 400 ~/.arc/token

# Монтируем arc репозиторий
shorrty@greed-ts1h.paysys ~ $ mkdir -p arc && cd arc
shorrty@greed-ts1h.paysys ~/arc $ mkdir -p arcadia store
shorrty@greed-ts1h.paysys ~/arc $ arc mount -m arcadia/ -S store/

# Проверяем, что смонтировалось
shorrty@greed-ts1h.paysys ~/arc $ cd arcadia/billing/agency_rewards/
shorrty@greed-ts1h.paysys ~/arc/arcadia/billing/agency_rewards $ arc log -n 1 .
commit 5ce436cfc34cf0b426676f8f4bed4227a6056c5c
merge: da613aeac600fed9a74c4f1a0c170952007fb2b1 ca435455061d4d36f1082e1198261727392cc361
author: shorrty
date: 2020-04-20T09:55:28+03:00
revision: 6678711

    Makefile: show-query теперь выводит запросы КО

    REVIEW: 1223464
```

Запуск регрессии (генерация данных, запуск расчета, проверка результатов):

```bash
# Открываем сессию screen, чтобы можно было пойти чаю попить, вернуться
# и (даже если пропадала сеть) увидеть результаты тестов
shorrty@greed-ts1h.paysys ~/arc/arcadia/billing/agency_rewards $ screen

# Где искать ya утилиту (через которую выполняется сборка и тесты. она лежит в корне аркадии)
shorrty@greed-ts1h.paysys ~/arc/arcadia/billing/agency_rewards $ PATH=$PATH:~/arc/arcadia

# Полный запуск
shorrty@greed-ts1h.paysys ~/arc/arcadia/billing/agency_rewards $ make regress-platform

# Запуск только тестов (без перегенерации данных и расчета)
shorrty@greed-ts1h.paysys ~/arc/arcadia/billing/agency_rewards $ make regress-platform-test

# Перезапуск расчета и запуск тестов (без генерации тестовых данных)
shorrty@greed-ts1h.paysys ~/arc/arcadia/billing/agency_rewards $ make regress-platform-calc
shorrty@greed-ts1h.paysys ~/arc/arcadia/billing/agency_rewards $ make regress-platform-test
```

Полезные ссылки:

- https://doc.yandex-team.ru/arc/setup/arc/install.html

### Запуск интеграционных тестов из ревью

Интеграционные тесты запускаются в рамках ревью (как и обычные юнит тесты).
Реализовано это следующим образом:
- https://wiki.yandex-team.ru/users/nozerchuk/arregressionteamcity/


### Как запустить конкретный тест

```sh
shorrty@greed-ts1v.paysys ~/arc/arcadia/billing/agency_rewards $ arc diff
--- billing/agency_rewards/Makefile     (index)
+++ billing/agency_rewards/Makefile     (working tree)
@@ -7,7 +7,7 @@ AR_CMD=./agency_rewards/main/yb-ar-calculate-bin
 CB_CMD=./cashback/bin/yb-ar-cashback
 PLOG=-= PLATFORM =-
 REG_TEST_DT=2020.03.03 11:11:11
-NOT_TESTED_THINGS=--no-mnclose --platform-calculation --no-plsql-calc --no-notifications --no-ok-check --platform-run-dt "${REG_TEST_DT}"
+NOT_TESTED_THINGS=--no-mnclose --platform-calculation --no-plsql-calc --no-notifications --no-ok-check --no-acts-yt-upload --platform-run-dt "${REG_TEST_DT}"
 YA_AR_INSERT_DT=$(shell date +"%Y.%m.%d %H:%M:%S")
 IPY_CMD=Y_PYTHON_ENTRY_POINT=:repl ${CONF} ${AR_CMD}


@@ -78,7 +78,7 @@ regress-platform-test-local: build
        @export YA_AR_REGRESSION=1 && \
        export YA_AR_TEST_PLATFORM=1 && \
        echo "--> [`date ${DT_FMT}`] ${PLOG} run tests ..." && \
-               ${CONF} ya make -ttt --test-tag large+ya:fat  && \
+               ${CONF} ya make -ttt --test-tag large+ya:fat -F 'tasks.test_balance34675.py::TestAddPaidPeriodsForPrepaid::test_check_paid_period_exists' && \
        echo "--> [`date ${DT_FMT}`] ${PLOG} done."

 #
--- billing/agency_rewards/agency_rewards/utils/platform.py     (index)
+++ billing/agency_rewards/agency_rewards/utils/platform.py     (working tree)
@@ -1019,6 +1019,8 @@ def fetch_all_bunker_calcs(bunker: BunkerClient,
     for n1 in bunker.ls(bunker.entry_point, shallow=True):
         log(f"fetched node: {n1.fullName}")
         for n2 in bunker.ls(n1.fullName):
+            if not n2.fullName == "/agency-rewards/dev/regression/tasks/balance-34675":
+                continue
             calc = BunkerCalc(
                 bunker.cat(n2.fullName, bunker.version_type),
                 bunker.env, opt.insert_dt, n2.name, n2.fullName,
```

### Как починить регрессию?

Если в ревью не отрабатывает регрессия, то помимо проблем в самих тестах, может быть проблема в окружении.
Ниже указаны основные проблемы и то, как их можно решить.

#### ORA-12154: TNS:could not resolve the connect identifier specified

Возможно, на том сервере, где запускались тесты, неправильно настроен Oracle Client.
Можно попробовать перезапустить несколько раз регрессию и посмотреть на результат.

Если ошибка стабильна, то идём её чинить:

- в логах обычно видно, по какому дескриптору пытались подключиться. например:
```shell
22-04-20 14:08:23,722 T:MainThread INF     billing.agency_rewards.agency_rewards.butils.dbhelper.helper: Creating new Oracle connection "oracle://bo:xxx@TEST_META_YANDEX_RU"
22-04-20 14:08:23,723 T:MainThread DBG     billing.agency_rewards.agency_rewards.butils.dbhelper.helper: connect_lock.acquire() succeeded, it took 0.000 sec.
Traceback (most recent call last):
...
  File "billing/agency_rewards/agency_rewards/butils/dbhelper/helper.py", line 171, in __create_oracle_connection
    conn = cx.connect(cx_dsn, threaded=True, **params)
cx_Oracle.DatabaseError: ORA-12154: TNS:could not resolve the connect identifier specified
```
- идём на сервер, где сломалось (имя хоста можно понять по агенту, на котором запускалась регрессия)
- смотрим, какой клиент используется:
```shell
shorrty@greed-dev3h.paysys ~ $ grep ORACLE_HOME= /etc/oraprofile
ORACLE_HOME="/opt/oracle/instantclient_19_3"
```
- проверяем, есть такой дескриптор в tnsadmin:
```shell
shorrty@greed-dev3h.paysys ~ $ grep TEST_META_YANDEX_RU /opt/oracle/instantclient_19_3/network/admin/tnsnames.ora | wc -l
0
```
- смотрим, откуда такой дескриптор появляется:
```shell
shorrty@greed-dev3h.paysys ~ $ grep TEST_META_YANDEX_RU /etc/yandex/balance-common/db-conn-meta.cfg.xml
        <Host>TEST_META_YANDEX_RU</Host>
```
- фиксим:
```shell
shorrty@greed-dev3h.paysys ~ $ sudo sed -i 's/TEST_META_YANDEX_RU/metadb.yandex.ru/g' \
    /etc/yandex/balance-common/db-conn-meta.cfg.xml
```


### Полезные запросы

```oracle-sql
-- результаты последнего расчета
select * from bo.t_comm_base_src where insert_dt = (select max(insert_dt) from bo.t_ar_run);

-- Данные кокнретного теста
select value from bo.t_ar_rgrs_data where class_name = 'TestEarlyPaymentWithExtraDiscountTypes' and field = 'contract_id1';

-- Тестовые премии из теста
select * from bo.t_ar_rgrs_rewards where contract_id = (select value from bo.t_ar_rgrs_data where class_name = 'TestEarlyPaymentWithExtraDiscountTypes' and field = 'contract_id1');
-- Тестовые акты из теста
select * from bo.t_ar_rgrs_acts where contract_id = (select value from bo.t_ar_rgrs_data where class_name = 'TestEarlyPaymentWithExtraDiscountTypes' and field = 'contract_id1');
-- Тестовые оплаты из теста
select * from bo.t_ar_rgrs_payments where contract_id = (select value from bo.t_ar_rgrs_data where class_name = 'TestEarlyPaymentWithExtraDiscountTypes' and field = 'contract_id1');
-- Тестовые выплаченные периоды из теста
select * from bo.t_ar_rgrs_paid_periods where contract_id = (select value from bo.t_ar_rgrs_data where class_name = 'TestEarlyPaymentWithExtraDiscountTypes' and field = 'contract_id1');
```


# market-loyalty

![статус сборки](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Abo_Pers_MarketLoyalty/statusIcon)

### Описание

Пользовательские купоны и акции

[Всякие диаграммы](docs/README.md)
[Кластер Wiki](https://wiki.yandex-team.ru/market/development/loyalty/)

### Адреса

[Тестовая админка](https://admin.market-loyalty.tst.market.yandex-team.ru/)

[Прод админка](https://admin.market-loyalty.market.yandex-team.ru/)

[API Reference (swagger)](http://market-loyalty.tst.vs.market.yandex.net:35815/swagger-ui.html)

### Мониторинги

#### market-loyalty

[Juggler](https://juggler.yandex-team.ru/dashboards/market-loyalty)

[Juggler, продуктовые мониторинги](https://juggler.yandex-team.ru/dashboards/market-loyalty-product-alerts/)

[Grafana timings and errors](https://grafana.yandex-team.ru/dashboard/db/market-loyalty?orgId=1)

[Grafana discounts](https://grafana.yandex-team.ru/d/bGdLdVbmz/loyalty-discount-metrics?orgId=1)

[Nginx-testing](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketloyalty;ctype=testing;prj=marketpers/)

[Nginx-production](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketloyalty;ctype=production;prj=marketpers/)

[Porto-testing](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketloyalty;ctype=testing;prj=marketpers/)

[Porto-production](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketloyalty;ctype=production;prj=marketpers/)

[Инстансы Grafana-production](https://grafana.yandex-team.ru/d/bspsIQGWz/markets-rtc-services-allocation-and-utilization?orgId=1&refresh=5m&from=now-24h&to=now&var-env=production&var-dc=ALL&var-hw_owner=market&var-category=market_pers_loyalty&var-func=0_95&var-top_exclude=report)

[Инстансы Grafana-testing](https://grafana.yandex-team.ru/d/bspsIQGWz/markets-rtc-services-allocation-and-utilization?orgId=1&refresh=5m&from=now-24h&to=now&var-env=testing&var-dc=ALL&var-hw_owner=market&var-category=market_pers_loyalty&var-func=0_95&var-top_exclude=report)

[jvm & jetty graphs - production](https://solomon.yandex-team.ru/?project=market-loyalty&cluster=agent-jvm-monitoring&service=agent-jvm-monitoring) - выбрать нужные

[jvm & jetty graphs - testing](https://solomon.yandex-team.ru/?project=market-loyalty-testing&cluster=agent-jvm-monitoring&service=agent-jvm-monitoring)

Запрос в CH:
```sql
select * from trace where target_module = 'market_loyalty' and environment='PRODUCTION' and date = '...'
```
#### market-loyalty-admin
[solomon](https://solomon.yandex-team.ru/admin/projects/market-loyalty)

#### База Postgresql

[![Схема PostgreDB (10.10.2020)](https://proxy.sandbox.yandex-team.ru/1777793894)](https://proxy.sandbox.yandex-team.ru/1777793894)

[Графики golovan, testing](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=c70abd77-5ad0-4e98-97f8-d9c47ea945ad;dbname=market_loyalty_test_db?range=86400000)

[Графики solomon, testing](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_c70abd77-5ad0-4e98-97f8-d9c47ea945ad&service=mdb&dashboard=internal-mdb-cluster-postgres)

[Графики golovan, load](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbs5a7e6h71uq77glms;dbname=market_loyalty_load?range=86400000)

[Графики solomon, load](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_mdbs5a7e6h71uq77glms&service=mdb&dashboard=internal-mdb-cluster-postgres)

[Графики golovan, production](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=815e033e-2584-4e12-a881-30161a6d67be;dbname=market_loyalty_prod_db?range=86400000)

[Графики solomon, production](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_815e033e-2584-4e12-a881-30161a6d67be&service=mdb&dashboard=internal-mdb-cluster-postgres)

[Управление, testing](https://yc.yandex-team.ru/folders/foo9089arq2rcch8gaip/managed-postgresql/cluster/c70abd77-5ad0-4e98-97f8-d9c47ea945ad)

[Управление, load](https://yc.yandex-team.ru/folders/foo9089arq2rcch8gaip/managed-postgresql/cluster/mdbs5a7e6h71uq77glms)

[Управление, production](https://yc.yandex-team.ru/folders/foo9089arq2rcch8gaip/managed-postgresql/cluster/815e033e-2584-4e12-a881-30161a6d67be)

[Графики, memcache, testing - количество элементов, размер кеша](https://grafana.yandex-team.ru/dashboard/db/market-memcached?refresh=1m&orgId=1&from=now-6h&to=now&var-group=%25market_cache-testing&var-port=21222)

[Графики, memcache, testing - get,set](https://grafana.yandex-team.ru/dashboard/db/market-mcrouter?refresh=1m&orgId=1&from=now-6h&to=now&var-group=%25market_cache-testing&var-port=11222)

slow query log можно посмотреть через yc

[Графики, memcache, production - количество элементов, размер кеша](https://grafana.yandex-team.ru/dashboard/db/market-memcached?refresh=1m&orgId=1&from=now-6h&to=now&var-group=%25market_cache-stable&var-port=21222)

[Графики, memcache, production - get,set](https://grafana.yandex-team.ru/dashboard/db/market-mcrouter?refresh=1m&orgId=1&from=now-6h&to=now&var-group=%25market_cache-stable&var-port=11222)

#### База Ydb
Всегда создавать таблицы с включенной опцией `AUTO_PARTITIONING_BY_LOAD`.

При ручных запросах на чтение через UI **ВСЕГДА** добавлять в начало `PRAGMA Kikimr.ScanQuery = "true";` во избежание влияния на метрики прода. Подробнее про это [тут](https://ydb.yandex-team.ru/docs/data_interfaces/scan_queries)

**ЖЕЛАТЕЛЬНО** также добавлять ко всем запросам `limit` и в случае сомнений попробовать сначала запрос на [prestable](https://ydb.yandex-team.ru/db/ydb-ru-prestable/marketloyalty/testing/market-loyalty/browser)

`explain plan` запроса можно посмотреть при помощи команды в консоли
```
ya ydb -e ydb-ru-prestable.yandex.net:2135 -d /ru-prestable/marketloyalty/testing/market-loyalty table query explain -t scan -f market2.sql
```

**ДЛЯ ВЫПОЛНЕНИЯ ТЯЖЕЛЫХ** запросов к базе вместо вышеуказанного способа лучше использовать копию YDB таблицы в YT.
Выгрузить копию таблицы в YT можно по [инструкции](https://ydb.yandex-team.ru/docs/maintenance/backup_and_recovery#yt_export)


[market-loyalty - YDB browser](https://ydb.yandex-team.ru/db/ydb-ru/marketloyalty/production/market-loyalty/browser)

[Тикет YDBREQUESTS](https://st.yandex-team.ru/YDBREQUESTS-193)

### Logbroker
[Топик market-loyalty в очереди событий чекаутер](https://lb.yandex-team.ru/lbkx/accounts/market-loyalty?page=browser&type=account&metricsFrom=1607004626509&metricsTo=1607091026509)


### Выкладка автоматическая

- автоматическая выкладка через
    [Пайплайн в Цуме](https://tsum.yandex-team.ru/pipe/projects/pers)

    Строго не рекомендуется снимать галочки с модулей при запуске пайплайна.

### Выкладка ручная

#### Тестинг

- liquibase
    ```bash
    ./gradlew :market-loyalty-db:liquibaseRun --command=update -Pmbuild.liquibase.runList=testing
    ```

##### Мастер
- market-loyalty и market-loyalty-admin

    [Джоба в TeamCity для market-loyalty (master)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_MarketLoyalty_MarketLoyaltyDeploy)

##### market-loyalty-common
Общий код который может использоваться в нескольких персональных сервисах вынесен в модуль market-loyalty-common

Чтобы обновить пакет нужно вручную запустить таску в [тимсити](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_MarketLoyaltyCommon)

##### Из ветки
- market-loyalty

    [Джоба в TeamCity для market-loyalty (ветка)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_MarketLoyalty_MarketLoyaltyDeployBranch)

- market-loyalty-admin

    [Джоба в TeamCity для market-loyalty-admin (ветка)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_MarketLoyalty_MarketLoyaltyAdminDeployBranch)

#### Прод

- liquibase

    ```bash
    ./gradlew :market-loyalty-db:liquibaseRun --command=update -Pmbuild.liquibase.runList=production
    ```

- market-loyalty

    [Таска в Sandbox для market-loyalty](https://sandbox.yandex-team.ru/resources/?type=MARKET_PERS_LOYALTY_APP&page=1&pageCapacity=20&attrs=%7B%7D)

- market-loyalty-admin

    [Таска в Sandbox для market-loyalty-admin](https://sandbox.yandex-team.ru/resources/?type=MARKET_PERS_LOYALTY_ADMIN_APP&page=1&pageCapacity=20&attrs=%7B%7D)

### Доступ в БД

Для получения доступа нужно сделать запрос в IDM и поискать явки-пароли в секретнице

#### Тестинг ####

* idm:  dbaas -> market_loyalty_test_cluster
* vault: https://yav.yandex-team.ru/secret/sec-01egmsak0yg7n257a36zj17ctx/explore/version/head

#### Load ###
* vault: https://yav.yandex-team.ru/secret/sec-01ewgcpebh8c0vfwqye9k54dwf/explore/version/head

#### Продакшен ####

* idm: dbaas -> market_loyalty_prod_cluster
* vault: https://yav.yandex-team.ru/secret/sec-01d7hmjyakd5ezcg9n0xcs454z/explore/version/head

### Прочее

[чек лист для ревью](reviewCheckList.md)

**конфиги:**
вносим изменения в конфигурацию Nanny, копируем задачу для сборки, указываем коммит и собираем.

**приложение:**
дергаем джобу в TeamCity, дожидаемся статуса ACTIVE в Nanny, если прошлый раз не стартовало - в Nanny нужно активировать вручную

[стрельбы](load.md)

**профилирование:**
для сбора статистики копируем collect_profile_back_prod.sh на braavos и запускаем
```bash
collect_profile_back_prod.sh > profile.html
```
профилировщик (trace sampling):
1. заходим на rtc машину по porto
2. cd external/async-profiler
3. run_on_rtc.sh [SECONDS_TO_PROFILE?:600]
4. в logs/market-loyalty/flame появится файл flamegraph_{date}.svg
5. скачиваем svg с logview, смотрим, к примеру, через chrome
Профилировщик имеет смысл запускать вместе со стрельбами - получиться понять на что именно уходит время
NOTE бинарник для профилировщика собран на braavos, гарантии что он будет работать вечно нет.

[Рекомендации по написанию тестов](testGuide.md)

**обновление dependencies.lock**
```bash
find . -name 'dependencies.lock' | xargs rm
./gradlew clean :market-loyalty-db:generateLock :market-loyalty-db:saveLock :market-loyalty-core:generateLock :market-loyalty-core:saveLock :market-loyalty:generateLock :market-loyalty:saveLock :market-loyalty-admin:generateLock :market-loyalty-admin:saveLock generateProto generateGrammarSource ngBuild -Plocal=true
```

Если приложение не поднимается, смотреть стоит:
- в loop.log и loop.log.full
- в market-loyalty.out и market-loyalty.err
- в logs/*


### Инфраструктура

[Группа в GenCfg (тестинг, Сасово)](https://gencfg.yandex-team.ru/unstable/groups/SAS_MARKET_TEST_PERS_LOYALTY)

[Группа в GenCfg (прод, Сасово)](https://gencfg.yandex-team.ru/stable-100-r30/groups/SAS_MARKET_PROD_PERS_LOYALTY)

[Группа в GenCfg (прод, Ивантеевка)](https://gencfg.yandex-team.ru/stable-100-r30/groups/IVA_MARKET_PROD_PERS_LOYALTY)

[Группа в GenCfg (прод, Владимир)](https://gencfg.yandex-team.ru/stable-100-r30/groups/VLA_MARKET_PROD_PERS_LOYALTY)

---

[Сервис в Nanny (тестинг, Сасово)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_loyalty_sas/)

[Сервис в Nanny (тестинг, Владимир)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_loyalty_vla/)

[Сервис в Nanny (прод, Сасово)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_loyalty_sas/)

[Сервис в Nanny (прод, Ивантеевка)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_loyalty_msk/)

[Сервис в Nanny (прод, Владимир)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_loyalty_vla/)

[Сервис в Nanny для market-loyalty-admin(тестинг, Сасово)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_loyalty_admin_sas/)

[Сервис в Nanny для market-loyalty-admin(тестинг, Владимир)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_loyalty_admin_vla/)

[Сервис в Nanny для market-loyalty-admin(прод, Сасово)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_loyalty_admin_sas/)

[Сервис в Nanny для market-loyalty-admin(прод, Ивантеевка)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_loyalty_admin_msk/)

---

[Конфиг сервиса в Nanny](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/pers/loyalty)

[Задача сборки конфига Nanny в Sandbox](https://sandbox.yandex-team.ru/task/102601631/view)

#### Логи

Логи доступны на сервере logview.market.yandex.net (доступен по ssh)

Перед грепом лучше перемонтировать каталоги:

```bash
sudo mount-service-log -o remount testing_market_loyalty_sas testing_market_loyalty_admin_vla testing_market_loyalty_vla production_market_loyalty_admin_sas production_market_loyalty_admin_msk testing_market_loyalty_admin_sas production_market_loyalty_sas production_market_loyalty_vla production_market_loyalty_msk
```

Пример грепа по всем бэкендам прода:

```bash
grep '1558532370980/120f8a33db8fd6c9a7874202eec426c7/3' /mnt/nanny/production_market_loyalty_*/*/market-loyalty/market-loyalty.log | less
```

[Архив логов(тестинг,sas1-2414)](https://logs.market.yandex.net/31214@sas1-2414.search.yandex.net)

[Архив логов(тестинг,sas1-2415)](https://logs.market.yandex.net/31214@sas1-2415.search.yandex.net)

[Архив логов(тестинг,vla1-4710)](https://logs.market.yandex.net/12920@vla1-4710.search.yandex.net)

[Архив логов(тестинг,vla2-8743)](https://logs.market.yandex.net/12920@vla2-8743.search.yandex.net)

[Архив логов(прод,sas1-2417)](https://logs.market.yandex.net/19235@sas1-2417.search.yandex.net)

[Архив логов(прод,sas1-8956)](https://logs.market.yandex.net/19235@sas1-8956.search.yandex.net)

[Архив логов(прод,sas3-0348)](https://logs.market.yandex.net/19235@sas3-0348.search.yandex.net)

[Архив логов(прод,sas3-0349)](https://logs.market.yandex.net/19235@sas3-0349.search.yandex.net)

[Архив логов(прод,iva1-0430)](https://logs.market.yandex.net/7490@iva1-0430.search.yandex.net)

[Архив логов(прод,iva1-0433)](https://logs.market.yandex.net/7490@iva1-0433.search.yandex.net)

[Архив логов(прод,iva1-0903)](https://logs.market.yandex.net/7490@iva1-0903.search.yandex.net)

[Архив логов(прод,iva1-3783)](https://logs.market.yandex.net/7490@iva1-3783.search.yandex.net)

[Архив логов(прод,vla1-4736)](https://logs.market.yandex.net/9930@vla1-4736.search.yandex.net)

[Архив логов(прод,vla1-5128)](https://logs.market.yandex.net/9930@vla1-5128.search.yandex.net)

[Архив логов(прод,vla2-8724)](https://logs.market.yandex.net/9930@vla2-8724.search.yandex.net)

[Архив логов(прод,vla0-6890)](https://logs.market.yandex.net/9930@vla0-6890.search.yandex.net)

[Архив логов(прод,vla0-6897)](https://logs.market.yandex.net/9930@vla0-6897.search.yandex.net)

[Архив логов админки(тестинг,sas1-2414)](https://logs.market.yandex.net/14328@sas1-2414.search.yandex.net)

[Архив логов админки(тестинг,sas1-2415)](https://logs.market.yandex.net/14328@sas1-2415.search.yandex.net)

[Архив логов админки(тестинг, vla1-4710)](https://logs.market.yandex.net/12713@vla1-4710.search.yandex.net)

[Архив логов админки(тестинг, vla2-8743)](https://logs.market.yandex.net/12713@vla2-8743.search.yandex.net)

[Архив логов админки(прод, sas1-2417)](https://logs.market.yandex.net/19090@sas1-2417.search.yandex.net)

[Архив логов админки(прод, sas1-8956)](https://logs.market.yandex.net/19090@sas1-8956.search.yandex.net)

[Архив логов админки(прод, iva1-0430)](https://logs.market.yandex.net/19110@iva1-0430.search.yandex.net)

[Архив логов админки(прод, iva1-0433)](https://logs.market.yandex.net/19110@iva1-0433.search.yandex.net)







### Локальный запуск

#### market-loyalty

Из корня репозитория:

```bash
cp market-loyalty/src/main/properties.d/local/local.properties.ex market-loyalty/src/main/properties.d/local/local.properties
./gradlew -Plocal :market-loyalty:run
```

  или если нужен запуск in-memory postgresql

```bash
./gradlew -Plocal -Pinmem :market-loyalty:run
```

Бэкэнд должен подняться на порту 8080.
Если in-memory postgresql не поднимается, то стоит проверить `/etc/hosts`,
`localhost` должен резолвиться и по IPv4 и по IPv6. Например

```
127.0.0.1   localhost
::1         ip6-localhost ip6-loopback localhost
```

#### Настройка локальной БД

Нужно добавить pgcrypto. Для этого:
```bash
psql -U postgres market_loyalty_db
```
```sql
create extension pgcrypto;
```
Первый пункт может отвалиться по authentication failed, тогда меняем в /etc/postgresql/{pgVersion}/main/pg_hba.conf
local   all             postgres                                peer
на
local   all             postgres                                trust


#### Настройка локальных логов
При запуске в конфигурации указать
```
    -Dlog4j.configurationFile=log4j2-test.xml
```

#### market-loyalty-admin

Смотри в [market-loyalty-admin](market-loyalty-admin/README.md)

### Схема данных

![market_loyaltydb_test](https://jing.yandex-team.ru/files/valter/diagram.png)

Для оптимизации прогона тестов на локальной машине можно добавить в файл `/etc/fstab` следующую строку:
```
inmemtmp /var/tmp/inmem tmpfs size=2G,uid=root,gid=root,mode=1777,relatime 0 0
```
Создать директорию `sudo mkdir /var/tmp/inmem`
Выполнить `sudo mount /var/tmp/inmem` (однократно, при следующей перезагрузке монтирование будет выполняться автоматически).
И в gradle передавать `-Djava.io.tmpdir=/var/tmp/inmem`, например:
```bash
./gradlew --parallel -Djava.io.tmpdir=/var/tmp/inmem test
```
или в Settings | Build, Execution, Deployment | Build Tools | Gradle | Gradle VM Options добавляем -Djava.io.tmpdir=/var/tmp/inmem
Также можно добавить параметр -Dbuild.develop=true для оптимизации сборки ts

### Аудит
Аудит ведется только в админке так целью аудита данных логирование данных которые меняют
пользователи. История изменений складывается в таблицы *_AUDIT.

### Ссылки
* [market-loyalty-admin](market-loyalty-admin/README.md)
* [Заглушка для тестирования ошибок market-loyalty](market-loyalty/stub.md)

###TMS

TMS - джобы, которые выполняют различную утилитарную работу (выгрузки в YT, чистку базы, импорт данных и т.п.)
Основной пакет с джобами `ru.yandex.market.loyalty.admin.tms`

У каждой джобы есть свое время запуска, которое настриваеся с помощью CRON нотации.

`ru.yandex.market.loyalty.admin.tms.ScheduledCron`

Логика работы реализована с помощью библиотеки Spring Scheduling.

Для работы в распределенной системе используется библиотека Schedlock, которая позволяет делать блокировки на конкретных
инстансах и не запускать параллельно одну и ту же джобу.

Информация о том, в какое время был последний запуск и будет следующий, а так же на каком хосту была блокировка
находится в таблице `shedlock`

Существует вспомогательная таблица `shedlock_history`

Она логирует все запуски всех джоб. Время старта и финиша. Текущий статус. Сообщение об ошибке, если таковая произошла,
а так же трассировку запуска.
Таблица хранит все запуски джоб за последний месяц.

Чистка этой таблицы происходит с помощью джобы `ru.yandex.market.loyalty.admin.tms.ShedlockHistoryCleanerExecutor`
, которая запускается раз в день.


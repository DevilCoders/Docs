# pers-grade

### Описание

Работа с отзывами
- api (pers-grade) - [Wiki](https://wiki.yandex-team.ru/market/development/pers/grade/)
- админка (pers-grade-admin, pers-grade-admin-view) - [Wiki](https://wiki.yandex-team.ru/market/development/pers/gradeadmin/)
- задачи по расписанию (pers-tms)

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

[API (тестинг)](http://pers-grade.tst.vs.market.yandex.net:35824/swagger-ui.html)

[Админка (тестинг)](https://admin.pers.tst.market.yandex.ru)

### Выкладка (RTC)

[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/market-pers-grade-arc)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-grade-branch)

[Релиз pers-grade-client](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_PersGrade_PersGradeClient)

[Выкатка liquibase](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-grade-liquibase)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### Nanny

[Nanny pers-grade](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_grade/)

[Nanny pers-grade-admin](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_grade_admin/)

[Nanny pers-tms](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_tms/)

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01f33qp2xtq2x016yz2m9nm7ca/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01f33qtz8jzd6z217895g8rzwr/explore/versions)

После изменения секрета можно накатить его через `persec grade test/prod`

Если ошибки с ssh, то стоит ввести команду: `ssh-add ~/.ssh/id_rsa`

### Графики

[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-grade)

[nginx метрики прода](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersgrade;ctype=production;prj=market/)

[proto метрики прода](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersgrade;ctype=production;prj=market/?range=21660000)

[pers-grade](https://grafana.yandex-team.ru/d/000001539/pers-grade?orgId=1)

[pers-grade-admin](https://grafana.yandex-team.ru/d/000001542/pers-grade-admin?orgId=1)

[статистика по отзывам](https://grafana.yandex-team.ru/d/000012033/pers-tms-grade-stats?orgId=1)

[больше статистики по отзывам](https://grafana.yandex-team.ru/d/000018139/pers-tms-grade-stats-temp?orgId=1)

[метрики индексации](https://grafana.yandex-team.ru/d/000016343/pers-grade-indexing-metrics?orgId=1)

[CPC-письма](https://grafana.yandex-team.ru/d/5RoaHQOik/cpc-mails-dashboard?orgId=1)

[Графики оракла](https://grafana.yandex-team.ru/d/000013702/oracle-database?orgId=1&from=now-7d&to=now&var-server=reviewdb01e_yandex_ru&var-server=reviewdb01f_yandex_ru&var-server=reviewdb01v_paysys_yandex_net&var-metric=All&var-instance=All&var-name=All&var-iface=All&var-disk=All&var-instance_metric=waclass_Commit&var-instance_metric=Database_Time_Per_Sec&var-cpu_metrics=All)

### Мониторинги
[CPC-письма в Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-ugc)

### Выгрузки таблиц
Основные таблицы: https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/pers-grade/tables

Описание: https://wiki.yandex-team.ru/market/development/pers/pers-grade-tables/

### Liquibase

Liquibase накатывается в пайплайне релиза.
Также есть отдельный пайплайн по накатыванию liquibase.
В любом случае, можно использовать скрипт `liquibase_pg.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc)
```
export GRADE_PG_DB_PWD_DEV=<значение из dev датасорцов>
export GRADE_PG_DB_PWD_TEST=<значение из dev датасорцов>
export GRADE_PG_DB_PWD_PROD=<значение из dev датасорцов>
```

Формат `./liquibase.sh <env> <command>`
- `<env>` - среда: devlight, dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh devlight update`


### Сборка и запуск

Сборка и прогон тестов `ya make -DUSE_PREBUILT_TOOLS --host-platform-flag=USE_PREBUILT_TOOLS -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)
В каждом из проектов есть локальные проперти `src/main/resources/properties.d/local/application-local.properties`.
Обычно они настроены достаточно для локального запуска сервиса, но могут быть исключения.

Где брать данные для запуска:
1. Секрет для TVM находится в [секретнице](https://yav.yandex-team.ru), в секрете PERS_TVM.
2. Токены и прочие секретные данные в [датасорцах](https://github.yandex-team.ru/cs-admin/datasources-ng-dev/blob/master/development/etcd.yml)
3. Секретница для [тестинга](https://yav.yandex-team.ru/secret/sec-01f33qp2xtq2x016yz2m9nm7ca/explore/versions)
4. Секретница для [прода](https://yav.yandex-team.ru/secret/sec-01f33qtz8jzd6z217895g8rzwr/explore/versions)

Специальные настройки, которые могут быть полезны:
* порт в проперти ```http.port``` в ```/src/main/properties.d/servant.properties```

**Важно**: для локального запуска нужно поднять локальную БД postgresql
```
# sudo -u postgres psql для локального подключения к БД
CREATE DATABASE pers_grade_db;
CREATE USER pers_grade WITH ENCRYPTED PASSWORD 'pers_grade';
GRANT ALL PRIVILEGES ON DATABASE pers_grade_db TO pers_grade;
ALTER USER pers_grade WITH SUPERUSER;
```

#### Локальный запуск через скрипт
Для запуска нужно сохранить несколько секретов в перменные окружения (удобно в .bashrc, чтобы не вводить каждый раз)
```
export GRADE_TVM_SECRET=<секрет из секретницы>
export GRADE_SERVICE_TVM_SECRET=<секрет из секретницы>
export GRADE_ADMIN_TVM_SECRET=<секрет из секретницы>
export YT_DEV_TOKEN=<взять dev токен к robot-pers-mds-dev из dev датасорцов>
```

Запуск приложения через скрипт `local-start.sh`, который есть в каждом из модулей (pers-grade, pers-grade-admin, pers-tms)
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую (не рекомендуется)
Локальный запуск - через класс:
* pers-grade - `ru.yandex.market.pers.grade.PersGradeMain`
* pers-grade-admin - `ru.yandex.market.pers.grade.admin.Launcher`
* pers-tms - `ru.yandex.market.pers.tms.Launcher`

Переменные окружения, которые нужно ввести в конфигурации idea
```
ENVIRONMENT=local
host.name=localhost
GRADE_TVM_SECRET=<секрет из секретницы>
GRADE_SERVICE_TVM_SECRET=<секрет из секретницы>
GRADE_ADMIN_TVM_SECRET=<секрет из секретницы>
YT_DEV_TOKEN=<взять dev токен к robot-pers-mds-dev из dev датасорцов>
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/grade/pers-grade/src/main/conf/local/log4j2-test.xml
```

### pers-grade

[API (тестинг)](http://pers-grade.tst.vs.market.yandex.net:35824/swagger-ui.html)

[Локальный swagger](http://localhost:8080/swagger-ui.html)

Логи в nanny по пути ```logs/pers-grade/pers-grade.log```


### pers-grade-admin

[API адмики (тестинг)](https://admin.pers.tst.market.yandex.ru/swagger-ui.html)

[Локальная админка](http://localhost:8080)

Логи в nanny по пути ```logs/pers-grade-admin/pers-grade-admin.log```

### pers-tms

Логи в nanny по пути ```/logs/pers-tms/pers-tms.log```

После запуска можно принудительно запустить конкретную джобу через telnet-консоль. После старта приложения в логах появится строчка ```[RemoteControlServer] Started remote control server in terminal pers-tms on port <port_number>``` К указанному порту (обычно это ```33906```) можно подключиться через telnet. Для этого нужно дождаться завершения инициализации приложения (в логах появятся записи про запущенный Quartz), затем подключиться через ```telnet localhost <port>``` и воспользоваться командами ```tms-list``` для получения списка джоб и ```tms-run``` для запуска.

Полезные команды:
* список готовых джоб `echo "tms-list" | nc localhost 33906`
* запуск джобы `echo "tms-run saasYtDumperExecutor" | nc localhost 33906`

При локальном запуске вместо полноценного планировщика кварца поднимается RAMScheduler, который работает вне кластера (чисто локально) без использования таблиц кварца в базе данных. При этом у всех джоб вне зависимости от конфигурации триггеров проставляется специальное крон выражение, которое, фактически, запрещает их автоматический запуск. Для запуска в ручном режиме нужно будет использовать интерфейс telnet или curl. Обычно это удобно для отладки конкретных джоб, чтобы другие не мешались. Если же хочется непременно запустить локально с настоящим кварцем, чтобы все джобы по-настоящему запускались в соответствии с расписанием, указанным в их триггерах, то в классах `GradeDatabaseSchedulerFactoryConfig` и `GradeRAMSchedulerFactoryConfig` в строке внутри аннотации `@Profile` нужно указать другое значение, отлично от `local`. Например, `dev`. Главное, потом это не закоммитить.

Удобно бывает смотреть, какие YQL запросы делал робот, особенно при локальной отладке.
Логин-пароль робота можно найти в секретнице в секрете с алиасом `pers.yandex.robots.credentials`
На деве используется робот `robot-pers-mds-dev`

### TVM
Есть ручки, закрытые TVM.
Для ручного доступа к ним нужно [получить роль](https://wiki.yandex-team.ru/passport/tvm2/getabcrole/) 'TVM ssh пользователь' в [marketpers](https://abc.yandex-team.ru/services/marketpers/)

Для генерации заголовка с токеном нужно использовать скрипт 'market/pers/common/src/main/bin/perstvm.sh grade <env>'

Сгенерированный tvm-тикет можно вставить как в курл, так и в сваггер.

### Репликация таблиц через ТМ 

Трансфер в тестинге https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/data-transfer/transfer/dttl890n96gog6ge66cs

Трансфер в проде https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/data-transfer/transfer/dtt7kc0jlo6sls19o453

ID трансферов
- тестинг dttl890n96gog6ge66cs
- прод dtt7kc0jlo6sls19o453

Для добавления новых таблиц нужно:
- выдать доступ пользователю
- добавить таблицу (или список) через апи https://cdc.n.yandex-team.ru/#/TransferService/TransferService_AddTables

Доступ проще всего выдавать на схему разом. Но нужно повторять при добавлении новых таблиц.
%%
GRANT SELECT ON ALL TABLES IN SCHEMA grade TO market_pers_grade_test_recplication;
GRANT SELECT ON ALL TABLES IN SCHEMA grade TO market_pers_grade_prod_replication;
%%

Список всех таблиц в трансферах, чтобы было удобно копипастить в АПИ.
Важно: отправляем только новые таблицы, иначе крупные таблицы типа grade будут загружены второй раз - это лишняя нагрузка на cpu.
Если добавление таблицы закончилось ошибкой - нужно не переактивировать трансфер из yc, а вызвать метод start из апи. Так репликация поднимется быстрее, не будет полного перекопирования данных.

```
{
  "tables": [
    "grade.grade",
    "grade.grade_shop",
    "grade.grade_model",
    "grade.grade_vote",
    "grade.karma_grade_vote",
    "grade.grade_factor",
    "grade.grade_factor_value",
    "grade.grade_photo",
    "grade.photo",
    "grade.aggr_grade_weight",
    "grade.ext_disabled_shops",
    "grade.ext_shop_own_region",
    "grade.ext_shop_without_rating",
    "grade.security_data",
    "grade.ungrouped_model",
    "grade.grade_import_partner_name",
    "grade.white_grade",
    "grade.mod_grade_last",
    "grade.model_vendor",
    "grade.model_category",
    "grade.yandex_models"
  ],
  "transfer_id": "dttl890n96gog6ge66cs"
}
```

Эти таблицы копировать не нужно, т.к. они регулярно перезагружаются полностью, это излишне повысит нагрузку на cpu БД при репликации, особенно в тестинге
```
    "grade.ext_mbi_shops",
    "grade.ext_mbi_datasource",
    "grade.ext_mbi_shop_param",
    "grade.ext_shop_business_id",
```

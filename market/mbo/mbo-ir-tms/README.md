# mbo-ir-tms

Сервис регулярных задач.

Выкладка пакетов происходит релизной машиной автоматически при мержах в trunk.
Релизная машина: https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-ir-tms-arc

### Прод

- Nanny: [SAS](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbo_ir_tms_sas/), [VLA](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbo_ir_tms_vla/)
- [Интерфейс](https://mbo.market.yandex.ru/ir-tms/manage-tasks.xml?use_filter=no)
- [Дашборд](https://mbo.market.yandex.ru/gwt/#dashboard)

### Тестинг

- Nanny: [SAS](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_mbo_ir_tms_sas/), [VLA](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_mbo_ir_tms_vla/)
- [Интерфейс](https://mbo-testing.market.yandex.ru/ir-tms/manage-tasks.xml?use_filter=no)
- [Дашборд](https://mbo-testing.market.yandex.ru/gwt/#dashboard)


## Запуск

### Сборка и запуск тестов

```sh
ya make -DJDK_VERSION=8 -ttt ir-tms .
```

### Генерация проекта

Для начала работы сгенерируйте проект с помощью команды

```sh
ya ide idea -DJDK_VERSION=8 --iml-in-project-root --project-root ~/arc/idea-projects/market/mbo/mbo-ir-tms

```

и откройте папку проекта в idea.
Данная подходит для структуры каталогов arc, описанной в [wiki](https://wiki.yandex-team.ru/users/sulim/howto/arc-directory-structure/).
Если вы используете другую структуру, замените `~/arc/idea-projects/market/mbo/mbo-ir-tms` на нужную папку.

## Локальный запуск

В идеале понадобится локально установленный постгрес, кликхаус и зукипер. От чего-то (или всего) из этого можно отказаться, если пользоваться разработческими или тестовыми сервисами. Но при этом важно понимать, что будет делать в них приложение при отладке, чтобы ничего не поломать при использовании общих сервисов. В разделе про датасорцы будет дано описание исходя из локальной установки этих сервисов. В случае использования общих сервисов надо будет сделать соответствующие изменения (то есть поменять адреса, порты, логины, пароли, названия баз).
Для локального запуска необходимо выполнить следующие шаги:

### 1. Копирование конфигурационных файлов с dev машинок.

Нужно скопировать datasources.properties и tnsnames.ora с, например, aida. Сделать это можно с помощью команд:

```
sudo mkdir -p /etc/yandex/market-datasources/ && scp aida.yandex.ru:/etc/yandex/market-datasources/datasources.properties ~ && sudo mv ~/datasources.properties /etc/yandex/market-datasources/datasources.properties
sudo mkdir -p /etc/oracle && scp aida.yandex.ru:/etc/oracle/tnsnames.ora ~ && sudo mv ~/tnsnames.ora /etc/oracle/tnsnames.ora
```

В скопированных в файл `/etc/yandex/market-datasources/datasources.properties` датасорцах надо сделать следующие изменения:

0. `market.zookeeper.connectString=localhost:2181` (если зукипер запущен на другом порту, то это надо учесть)
0. `mbo.clickhouse.cluster=` (то есть пустая строка в качестве значения), `mbo.clickhouse.host=localhost`, `mbo.clickhouse.password=` (пустая строка в качестве пароля), `mbo.clickhouse.username=default` (если для доступа к кликхаусу нужно использовать другие логин и пароль, то это нужно учесть)
0. аналогично `mbo.glstat.clickhouse.cluster=`, `mbo.glstat.clickhouse.host=localhost`, `mbo.glstat.clickhouse.password=`, `mbo.glstat.clickhouse.username=default`. Важно оставить `mbo.glstat.clickhouse.db=glstat` и создать в кликхаусе эту базу с помощью команды `create database glstat;`, выполненной в клиенте clickhouse, поскольку это название фигурирует не только в проперте, но и захардкожено где-то в исходниках проекта.
0. `mbo.pg.password=market_backoffice_local`, `mbo.pg.url=jdbc:postgresql://localhost:5432/market_backoffice_local`, `mbo.pg.userName=market_backoffice_local` (логин, пароль и название базы зависит от настроек используемого постгреса)

Затем в папке [properties.d](https://a.yandex-team.ru/arc_vcs/market/mbo/mbo-ir-tms/ir-tms/src/main/properties.d) нужно выполнить следующие команды:

```
ln -s /etc/oracle/tnsnames.ora tnsnames.ora
ln -s /etc/yandex/market-datasources/datasources.properties datasources.properties
```

### 2. Загрузка локального индексатора

*NB: Этот шаг должен выполняться автоматически, но по каким-то причинам при скачивании ресурса не срабатывает авторизация.*

Для этого нужно:

0. Создать папку для хранения индексера с названием `standalone-indexer`, лучше всего в папке с проектом.
0. Определить `${resource-id}` индексера на основе property `mbo.saas.standalone_indexer.resourceId` (см. файл `datasources.properties`, скопированный ранее).
0. Загрузить в созданную папку standalone indexer с именем файла `standalone_indexer-${resource-id}` (скачать можно по ссылке вида `https://sandbox.yandex-team.ru/resource/${resource-id}/view`).
0. Создать файл-маркер с помощью команды `touch standalone_indexer-${resource-id}-ok`.

### 3. Добавить в конфигурацию запуска следующие параметры

Добавить дополнительные параметры в конфигурацию запуска для класса [MboIrTmsMain](https://a.yandex-team.ru/arc_vcs/market/mbo/mbo-ir-tms/ir-tms/src/main/java/ru/yandex/market/ir/tms/MboIrTmsMain.java):

```
-Dconfigs.path=${ARCADIA_ROOT}/market/mbo/mbo-ir-tms/ir-tms/src/main/properties.d
-cp $Classpath$;${ARCADIA_ROOT}/market/mbo/mbo-ir-tms/ir-tms/src/main/conf/local;${ARCADIA_ROOT}/market/mbo/mbo-ir-tms/ir-tms/src/main/conf
-Denvironment=development
-Dspring.profiles.active=yt
-Dindexer.type=stratocaster
-Ddata.dir=$PROJECT_DIR$/data
-Doracle.net.tns_admin=${ARCADIA_ROOT}/market/mbo/mbo-ir-tms/ir-tms/src/main/properties.d
-Dmbo.saas.standalone_indexer.base_path=$PROJECT_DIR$
-Daccumulator.priceStats.yt.dirPath=//tmp/${USER}/price_stats
```

Чтобы это работало, надо заменить вхождения `${ARCADIA_ROOT}` на путь до локальной папки, куда примонтирована аркадия, а `${USER}` на логин на стаффе (в принципе, значение для `accumulator.priceStats.yt.dirPath` можно выбрать какое-то другое. Главное, чтобы у приложения был доступ на запись в эту папку в YT, если планируется проверять соответствующие функции, которые используют `accumulator.priceStats.yt.dirPath`).

При таком способе запуска, к сожалению, могут быть проблемы с исключением из classpath лишних библиотек, явно исключаемых с помощью exclude в ya.make. То есть они могут не исключиться (см. подробнее в тикете [DEVTOOLSSUPPORT-11615](https://st.yandex-team.ru/DEVTOOLSSUPPORT-11615)). Если это не помешает локальному выполнению приложения, то хорошо, но если помешает (будут всякие странные ошибка типа stackoverflow при логировании или отсутствия у того или иного класса какого-то метода), то можно действовать по-другому. Находясь в папке [ir-tms](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-ir-tms/ir-tms) данного проекта выполнить команду для сборки и команду для запуска приложения через консоль:
```
ya make -DJDK_VERSION=8
ARCADIA_ROOT=/home/semin-serg/arc/arcadia ./bin/ir-tms-local-start.sh --environment=development --debug=-agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=33197
```
Как и ранее, значение в переменной `ARCADIA_ROOT` должно соответствовать пути до локальной папки, куда примонтирована аркадия. Вместо порта 33197 можно использовать любой другой свободный порт, важно только потом указывать его же при определении конфигурации запуска в idea. В указанном варианте запуска java сразу после инициализации будет ждать подключения отладчика - это происходит благодаря параметру `suspend=y`. Пока отладчик не подключится - никакого прикладного кода (включая инициализацию контекста спринга) выполняться не будет. Это удобно в том случае, если хочется отлаживать какие-то базовые вещи, которые происходят на запуске приложения, например, инициализцию контекста спринга. Если же при отладке это не интересует, то можно выставить `suspend=n`, в результате чего прикладной код начнёт выполняться без ожидания подключения отладчика (хотя возможность подключиться позже всё ещё остаётся). Для подключения с помощью отладчика в IntelliJ IDEA должна быть определена конфигурация запуска, которая выглядит примерно так, как на [этом](https://jing.yandex-team.ru/files/semin-serg/Selection_1110.png) скриншоте. В виде xml-файла в папке с проектом это выглядит как-то [так](https://paste.yandex-team.ru/5621636). При таком способе запуска (из командной строки) приложение будет писать логи в файл `build/log/ir-tms.log` (путь указан относительно папки [ir-tms](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-ir-tms/ir-tms)).

### 4. Запустить необходимые задачи
В окружении `environment=development` приложение `mbo-ir-tms` переопределяет крон-выражение всем сконфигурированным задачам таким образом, чтобы они не запускались автоматически. Это сделано для удобства, поскольку при локальном запуске обычно хочется отлаживать какую-то определённую задачу и делать это контролируемо (то есть запускать вручную), а запуски других задач могут мешать (например, засорять логи). Для ручного запуска задач в запущенном приложении можно использовать telnet интерфейс. Для этого надо подключиться к приложению через telnet с помощью команды `telnet localhost 31656` (31656 - это порт, указанный в проперте `telnet.port`. При необхрдимости его можно поменять там и соответственно использовать другой порт при запуске telnet). После подключения можно использовать команду `tms-list` для вывода списка сконфигурированным джоб и команду `tms-run <название джобы>` для запуска определённой джобы (например, `tms-run dummyExecutor`). Более подробную информацию о доступных командах в telnet-интерфейсе можно получить, если выполнить в нём команду `help`. Также стоит отметить, что в окружении `environment=development` кварц в качестве движка использует ram-scheduler, то есть записи истории запусков задач в базу данных не производится. При подключении нескольких приложений `mbo-ir-tms` к одной и той же базе данных планировщики кварца будут работать независимо (не будут мешать и как-либо влиять друг на друга).


## Запуск на удаленном сервере

Для запуска ir-tms на удаленном сервере есть набор скриптов, которые используют тулзу [dev_uploader](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/devops/tools/dev_uploader).
Перед началом работы рекомендуются ознакомиться с [документацией к dev_uploader](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/devops/tools/dev_uploader/README.md) и выполнить первоначальную неастройку.

- `scripts/dev/build-ir-tms.py` - Собирает ir-tms, загружает его на удаленный сервер и устанавливает в папку dev.
- `scripts/dev/run-ir-tms.py` - Запускает ir-tms на удаленном сервере.
- `scripts/dev/stop-ir-tms.py` - Останавливает ir-tms на удаленном сервере.

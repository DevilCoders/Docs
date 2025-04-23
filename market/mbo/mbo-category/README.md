Интерфейс для работы с ассортиментом
====================================
 
Ссылки:
- https://cm.market.yandex-team.ru - прод
- https://cm-testing.market.yandex-team.ru - тестинг

Релизы катаются по зеленому транку и выкатываются релизной машиной:
https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-category-arc  
Фронт разрабатывается в репозитории: https://github.yandex-team.ru/market-java/mbo-category-frontend/

Разработка
----------------
#### Разработка в аркадии

##### Ссылки:
- Сборка Java в Аркадии: https://docs.yandex-team.ru/ya-make/manual/java/
- ya make -t: тестирование: https://docs.yandex-team.ru/ya-make/manual/tests/java
- Инструменты для облегчения работы с аркадией и арком: https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi-tools/arcadia

##### Релизные машины для аркадии:
- https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-category-arc
- https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-mdm-app-arc

##### Настройка arc:
- Установка/настройка arc: https://docs.yandex-team.ru/devtools/intro/quick-start-guide
- Конфигурация IDE: https://doc.yandex-team.ru/arc/setup/arc/ide.html
Там-же много другой полезной информации по работе с arc

По документации устанавливаем arc, монтируем, ставим плагин для idea.

Выполняем `bin/create-idea-project-with-libs.sh` (чтобы сборка прошла удалённо можно выполнить `bin/create-idea-project-with-libs.sh --dist`). В этом же скрипте есть более детальная команда, если хочется особенного.

После чего проект можно будет открыть идеей из папки `idea ~/IdeaProjects/mbo-category/`.
Можно настроить путь `IdeaProjects` через `export ARC_PROJECTS_ROOT=...` в `~/.profile`). 

##### Локальная сборка, запуск тестов:
- **ya make** - собрать модуль, в директории которого в данный момент находимся
- **ya make -t** - запустить тесты модуля, в директории которого в данный момент находимся (-t: small, -tt small+medium, -ttt small+medium+large)
- Если хотим, чтобы сборка выполнялась в облаке(выполняется быстрее), то добавляем аргумент **--dist**
- Если хотим запустить тесты в облаке, то надо указать таргет платформу: **-target-platform linux**
- Если нужно получить на локальную машину артефакты сборки/выполнения тестов, то добавляем аргумент **-E**
- Если при локальном запуске тестов возникают timeout-ы, то можно их проигнорировать, добавив аргумент **--test-disable-timeout**
- Для передачи аргументов jvm: **--jvm-args="-Darg=val"**

Тесты на ручки не включены в RECURSE_FOR_TESTS, поэтому для их запуска нужно перейти непосредственно в папку с тестами: `cd mboc-integration-tests/src/integration-test && ya make -ttt`

##### Локальный запуск:
1. Можно запускать из idea. Открываем `MboCategoryApplication` и запускаем проект (в настройках конфигурации не забудьте указать VM options: `-Dconfigs.path=${ARCADIA_ROOT}/market/mbo/mbo-category/mboc-app/src/main/properties.d`)
2. Для запуска из консоли: Выполняем ya make из директории модуля (например mboc-app). Появляется папочка bin, где будет находиться скрипт для запуска на локальной машине. Используем его. Например `cd mboc-app && ya make && ./bin/mboc-app-local-start.sh`

Так же см. https://wiki.yandex-team.ru/users/s-ermakov/Lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit

##### Если нужно обновить версию контриба, но такого в аркадии нету:
1. Выполняем **ya maven-import groupId:artifactId:version**, после чего в локальном arc импортируется нужный контриб и его транзитивные зависимости. Например: `ya maven-import ru.yandex:common-framework-lite:6922204`
2. Обновляем в зависимостях проекта версию, от которой теперь будем зависеть (обычно это делается в contrib.ya.make)
3. Делаем коммит/PR
4. Если контрибы новые, а не обновление существующих, то они должны пройти процесс согласования: https://clubs.at.yandex-team.ru/arcadia/18174

При обновлении зависимостей надо перегенерировать **ya ide idea**, либо запускать из идеи **Build -> Regenerate and reload: ya ide**, иначе idea не подхватит новые зависимости.


#### Локальный запуск
1. При локальном запуске, а также при прогоне интеграционных тестов приложение само ходит в *etcd* за датасорсами.
Но креденшены для доступов все же нужно один раз настроить.
Для этого в `~/.bash_profile` (для Ubuntu в `~/.profile`) на ноутбуке пишем следующие строки: 
```bash
export ETCD_USERNAME=datasources_read_all
export ETCD_PASSWORD="<password>"
```
, где `<password>` (и, если надо, username) нужно взять из конфигов confd с дев машинки. Например, с помощью такой команды: `ssh aida.yandex.ru "sudo cat /etc/confd/confd.toml"`.
2. Перезапускаем IDEA!
3. Открываем `MboCategoryApplication` и просто запускаем из IDEA (она автоматом подхватит конфигурацию Spring Boot). Приложение должно подняться на 8080 порту.
4. Устанавливаем сертификат в java https://wiki.yandex-team.ru/security/ssl/sslclientfix

#### Локальный запуск без ya make
Почему? Так быстрее запускается, удобнее работать. Но чуть больше действий.
1. Делаем п. 1-2 выше.
3. Делаем конфигурацию на запуск `MboCategoryApplication` (можно просто через Ctrl+Shift+F10 в нём)
4. Меняем её, добавляя:
  - VM Options: `-Dconfigs.path=${ARCADIA_ROOT}/market/mbo/mbo-category/mboc-app/src/main/properties.d`
  (по умолчанию идея делает конфигурацию с запуском в корне проекта).
5. Выставляем переменную data.dir=<path to project>/mbo-category/data-getter для properties.d/local/<you local conf>

#### Локальная БД
Ниже описан вариант через докер - отдельным контейнером.

Простой вариант при старте через идею - добавить `-Dlocal-pg=true`.
Параметры соединения:
- port: `cat ~/.embedpostgresql/local-pg.port`
- user: minipgaas
- password: nacc6opq

БД будет пустой. TODO: сделать скрипты, чтобы приносить нужные таблицы из нужного окружения (с slave-серверов (!)).

#### Локальный запуск MDM
Все точно так-же как при локальном запуске КИ только вместо `MboCategoryApplication` нужно запускать `MdmApplication` 

#### Локальный запуск КИ вместе с MDM
Пока мы полностью не оторвали MDM от КИ для локальной работы КИ нужен локально запущеный MDM который смотрит на ту же PostgreSQL базу
Сейчас КИ при локальном запуске настроен искать MDM на localhost:8081 и смотрит на ту же MDM базу

1. Настраиваем локальный запуск MDM см выше.
2. Запускаем локально MDM, 
3. Запускаем локально КИ

Если произошел конфикт портов, то в Run конфигурации Idea для MDM на вкладке VM Options добавляем -Dhttp.port=8081 для старта MDM на 8081 порту.

#### Локальный запуск с поддержкой TVM
1. Необходимо поменять профили бинов ru.yandex.market.mbo.mdm.common.config.TvmConfiguration.tvmClient,
или запуститься с профилем, отличным от local
2. В classpath необходимо добавить нативную библиотеку libticket_parser2_java.dylib. 
Это можно сделать добавив библиотеку в расширения java (в переменной java.library.path указан список путей до библиотеки)
или в настройках проекта.

#### Локальный запуск и выгрузки
По умолчанию локально, если ничего не делать, `StuffModelsService` запустится с пустым хранилищем, и это будет означать постоянные походы в `getModels/findModels`.
**Что вполне ок для разработки**.

Если всё же нужны выгрузки:
1. Идём в SandBox и ищем ресурсы [MARKET_DATA_MBO_CATEGORY](https://sandbox.yandex-team.ru/resources/?type=MARKET_DATA_MBO_CATEGORY&page=1&pageCapacity=20)
2. Скачиваем последний для нужной среды (stable/testing) и разархивируем в корень, в `data-getter` папку. Так, чтобы получилось `data-getter/mbo-category/...`.
3. Для запуска стоит, чтобы наверняка, прописать в свойства `ext.data.dir=/home/..../absolute-path-to-data-getter-dir`.

#### Возможные ошибки при запуске и способы их решения
- Если возникает [такая](https://paste.yandex-team.ru/688972) ошибка при старте приложения,
 то необходимо скачать [этот](https://yadi.sk/d/NfovMLwLk2jI6A)
 архив и положить оба файла из него туда, где джава их увидит (например, /usr/lib/ для линукса),
 затем обновить кэш статических библиотек выполнив sudo ldconfig. <br />
 Для mac OS готовую библиотеку можно скачать [тут](https://wiki.yandex-team.ru/users/mors741/tvm-ticketparser2java-lib-from-sources/#gotovajalibapodmacos), положить ее надо в /Library/Java/Extensions  

#### Подключение к базе данных
Через Идею
1. Идем в `Help/Edit Custom VM Options` и убираем строчку `-X:PreferIPV4=true`   
2. Через Database создаем новый DataSource PostgreSQL
3. Host, Port, DB, User - вот тут https://st.yandex-team.ru/CSADMIN-22649 (в комментах), 
   но для дева и тестинга хост на самом деле `pgaas-test.mail.yandex.net`
4. В настойках SSH/SSL включить SSL и добавить `CA file`(он уже должен быть на устройстве, 
   но можно и скачать отсюда https://nda.ya.ru/3S7n2k)
5. Для прода также придется врубить SSH туннель 
    - `Host`: aida
    - `User`: твой пользователь
    - `Auth type`: Key Pair
    - `Private key file`: путь до приватного ключа
    - `Passphrase`: пароль от приватного ключа
6. Схема `mbo_category`

#### Дополнительно 

Swagger: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html) - можно смотреть, какие есть API, пробовать их и т.п.

Разные API:
- /api - все наши внутренние API, поддерживаем совместимость только внутри приложения
- /api/external - тут не проверяются доступы - это штуки, доступные извне, поддерживаем совместимость
- /proto - прото ручки, также, не проверяются доступы, доступно извне, поддерживаем совместимость

Глоссарий
---------
- `3P поставщик` - "третья сторона" - торгует с нашего склада, но товары принадлежат ему
- `1P поставщик` - "от первого лица" - мы покупаем у него товары и торгуем сами (товары наши, учитываются в ERP, Axapta)
- `supplier_id` - id поставщика из выгрузки MBI - там будут и 3P и 1P поставщики
- `shop_id` - id магазина, по сути у нас - id поставщика, они берутся из одного sequence-а, но хранятся в разных таблицах
- `real_supplier_id`, он же `rs_id` - id 1P поставщика из Axapta, текстовый (до 20-ти символов)
- `MSKU` - маркетное SKU, наше
- `SSKU` - shop sku, SKU от 3Р поставщика
- `RSSKU` - aka real supplier sku - это sku от 1P поставщика, при этом для них в качестве SSKU мы используем связку SSKU = "RS_ID.RSKU"
- `shop_sku` - в нашей БД мы храним shop_sku, которые для 3P являются SSKU, для 1P - RSKU

Разбивка по модулям/пакетам:
------------
- [mboc-common](./mboc-common) - там почти всё приложение - т.к. у нас потенциально сейчас две "головы" - mboc-app и mboc-tms, то общие вещи 
  (конфигурация БД, доступ к БД, общие сервисы) живут в common... это такой mbo-core, к сожалению. Там же живут интеграционные тесты всего этого дела (со своим конфигом)
- [mboc-tms](./mboc-tms) - TMS-ная часть - то, что только TMS, вызывается по расписанию. Со временем уедет в отдельное приложение. Пока что работает в контексте mboc-app.
- [mboc-app](./mboc-app) - приложение, веб-часть, там же фронтенд в [src/frontend](./mboc-app/src/frontend). Там живут контроллеры и прочее, 
  что нужно для прокидывания данных в/из веба.
  
Запуск тулов
------------
Вариант для бедных, см. [MboCategoryApplication.checkToolRun](mboc-app/src/main/java/ru/yandex/market/mboc/app/MboCategoryApplication.java).

Пишется компонент-тул, запуск - через переменную окружения `mboc_run_tool`

Миграции/локальный PGaaS
------------------------
- На проекте подключен Liquibase для накатки миграций, миграции в [mboc-common/src/main/resources/sql/mbo_category_common.xml](mboc-common/src/main/resources/sql/mbo_category_common.xml).
- Новые накатываются автоматически при старте приложения
- Откатывать миграции можно еще немного поднастроив mbuild-liquibase

При разработке новых миграций, особенно тех, что ломают работу другим на development базе (rename-ы колонок/таблиц), удобно использовать локальный PG:
- Залогиниться в докер, инструкция тут: https://wiki.yandex-team.ru/qloud/docker-registry/#avtorizacija
```bash
sudo docker login -u <domain-login> -p <token> -e <domain-login>@yandex-team.ru registry.yandex.net/dbaas/minipgaas
```    
token - взять отсюда https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1

- Запустить докер (c ```sudo```, если нет прав для сокетов):
```bash
docker run -p 12000:12000 \
    -e OPT_pgbouncer_max_client_conn=10000 \
    -e OPT_pre_sql='CREATE EXTENSION pg_trgm;' \
    -t -i registry.yandex.net/dbaas/minipgaas
```
Здесь специально создается экстеншн, иначе скрипты будут падать.

- Для того, чтобы ваше приложение смотрело локальную БД необходимо добавить датасорсы 
`properties.d/local/90.sql.local.properties` такого вида:
```properties
sql.url=jdbc:postgresql://localhost:12000/database
sql.userName=minipgaas
sql.password=nacc6opq
```

Как работает/отлаживать авторизацию локально
--------------------------------------------
Как работает авторизация:
- есть яндекс-тимовая кука, session2, на .yandex-team.ru
- с нею мы ходим в BlackBox и получаем логин пользователя и вообще, жива ли она
- если её нет - шлём пользователя авторизовываться

Чтобы проверить её по настоящему локально есть нюансы:
1. Чтобы это работало - локально тоже должен быть .yandex-team.ru домен, например, прописать в /etc/hosts `127.0.0.1   cm-local.market.yandex-team.ru`
2. Кука - secure, т.е. нужно локально ходить по https 
    - (и в инкогнито, чтобы браузер забыл про HSTS и принял самоподписанный сертификат)
    - и без webpack-а, т.к. тамошний сертификат - на localhost
3. BlackBox банит ноутбуки (м.б. можно сделать дырку), самое быстрое - пробросить через aida `ssh -L 8001:blackbox.yandex-team.ru:80 aida.yandex.ru`
4. Если так пробросить - то надо не забыть выставить Host заголовок, иначе 404
5. ip-шник должен быть не локальным, но локально будет 127.0.0.1

В общем, ничего невозможного, но геморно. Простой путь - `mboc.auth.debug_user` по умолчанию будет брать текущего пользователя,
т.е. по идее всё должно просто работать.

Если надо что-то локально поотлаживать в этом пути - надо скопировать local/60-dev-ssl-auth.local.properties.sample и запускаться с ним (стоит его почитать). 


Несколько соображений на тему client-side-а (для истории)
---------------------------------------------------------
Бэкграунд: это первый, но не последний проект с React-ом у нас, поэтому думаем на вырост, и обкатываем решения.

Хотелки:
- для большой кодовой базы хочется иметь типизацию - TypeScript или Flow
- пока что - TypeScript, потому что:
  - больше тайпингов в интернетах
  - для Flow весьма странный тулинг - идея что-то показывает, что-то нет, хуже дела с рефакторингами
- Webpack - неизбежность, хочется:
  - всяких штук, вроде hot reload (хотя бы для css, и рефреша для кода)
  - рабочих тестов из коробки (чтобы брать и писать, а не настраивать)
  - того же typescript-а
- Не хочется:
  - кучи разных немного отличающихся конфигов Webpack-а в разных модулях
- поэтому есть большое желание завязаться на create-react-app с минимальными модификациями (или вообще без оных)


Получение хостов для PGaaS
--------------------------
* `yc mdb cluster ListHosts --clusterId c784a5a1-f32f-4408-b178-5509da6ba3ab | jq .hosts[].name`
* id кластеров смотрим тут: https://st.yandex-team.ru/CSADMIN-22649 (в ссылке на графики)
* инфа про `yc mdb`: https://wiki.yandex-team.ru/MDB/quickstart/
* нужно быть в ABC в группе https://abc.yandex-team.ru/services/marketdbops/

#### Подключение расширений для базы данных
Так как у нас кластеры постгреса в облаке, придется выполнить несколько операций 
(Просто `create extension` в ликвибейзе не пройдет, прав не хватит)
1) Получить роль разработчика в https://abc.yandex-team.ru/services/marketdbops/
2) Поставить yc CLI: https://doc.yandex-team.ru/cloud/mdb/quickstart.html
3) https://iam.cloud.yandex.net:14222/v1/mapping/abc/services/2316 взять отсюда "yc_project_id"
4) Найти кластера: cм. Получение хостов (или `yc mdb cluster List --projectId 183ec711-e889-4f1a-9ac3-0a2b51abfe1f`)
5) Добавить расширение yc mdb cluster AddExtension --clusterId=<идентификатор кластера> --name <Имя расширения>
6) Добавить ликвибейз-скрипт 
```sql
 create extension if not exists <Имя расширения>;
```
Скрипт в ликвибейзе нужен для того, чтобы тесты не падали.
При использовании BaseDbTest или BaseIntegrationTest создается чистая база,
если не накатить скрипт с расширением, будут падать скрипты с функициями из расширений.
Для боевых баз расширения уже стоят, поэтому ликвибейз их не будет накатывать.

Если нужно добавить скрипт в локальный PGaaS, то нужно либо подключать расширение при старте,
либо получать права суперюзера:
```bash
docker run -p 12000:12000 \
    -e OPT_pgbouncer_max_client_conn=10000 \
    -e OPT_pre_sql='CREATE EXTENSION <Имя расширения>;' \
    -t -i registry.yandex.net/dbaas/minipgaas
```
```bash
docker run -p 12000:12000 \
    -e OPT_pgbouncer_max_client_conn=10000 \
    -e OPT_db_grants=SUPERUSER \
    -t -i registry.yandex.net/dbaas/minipgaas
```

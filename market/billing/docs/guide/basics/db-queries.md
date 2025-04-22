# Запросы в БД

Цель: делать запросы в наши БД

## Общая информация { #general-info }

### Про работу с БД через Idea { #idea }

Открыть окно с подключениями: меню View / Tool Window / Database

Начать создавать новое подключение: нажать кнопку "+" в окне Database,
выбрать пункт Data Source и дальше Oracel или PostreSQL.

Как заполнить настройки &mdash; см. ниже в соответствующих разделах.

В конце полезно нажать `Test Connection`. Если закончится с ошибкой &mdash; разбираться.

Если ошибка - "java.rmi.ConnectException: Connection refused to host: ::1" или "java.rmi.ConnectException: Connection refused to host: 127.0.0.1", то вероятно вам поможет [этот рецепт](https://wiki.yandex-team.ru/market/development/infra/tsum/relizy/firststeps/#oshibkipodsoedinenijakbdvdatagripilividea).

### Про работу с Postgres через psql (cli-клиент) { #psql }

Установить на Ubuntu: `sudo apt-get install postgresql-client-9.5`
Установить на Mac OS X: `brew install postgresql`

### Про работу с Oracle через Idea / DataGrip { #oracle }

Для каждого подключения надо создать каталог (обыкновенный каталог на локальном диске) и в нем создать файл `tnsnames.ora`.
Как заполнить файл для каждой БД см. ниже в соответствующих разделах.

Где создавать каталоги и как их называть &mdash; неважно, но удобно организовать их в структуру такого типа:

```
/home/<login>
  /market-billing-oracle
    /dev
      /tnsnames.ora
    /test
      /tnsnames.ora
    /prod
      /tnsnames.ora
```

**ВАЖНО:** проверьте через свойства файла или терминал, что `tnsnames.ora` называется в точности так, без дополнительных `.txt`.

### Про работу с Postgres { #postgres }

Наши кластера в интерфейсе MDB: <https://yc.yandex-team.ru/folders/foofljs7dr5uhp54fh22/managed-postgresql>

Для каждого кластера есть специальный fqdn, который всегда указывает на текущего мастера ("волшебный dns").
Конструируется так: `c-<идентификатор кластера>.rw.db.yandex.net`

Идентификатор кластера -- из интерфейса MDB.


## Настройки для конкретных БД и вариантов подключений

### Oracle, Idea, разработческая БД

Выше в разделе Общая информация см. инструкции где найти настройки подключений в БД в Idea и что такое tnsnames.ora.


Файл tnsnames.ora:

```
BILLINGDEV01.YANDEX.RU =
   (DESCRIPTION =
            (ADDRESS_LIST =
              (ADDRESS = (PROTOCOL = TCP)(HOST = mdbaas-sas-scan.paysys.yandex.net)(PORT = 1521))
              (ADDRESS = (PROTOCOL = TCP)(HOST = mdbaas-vla-scan.paysys.yandex.net)(PORT = 1521))
            )
          (CONNECT_DATA =
        (SERVER = DEDICATED)
      (SERVICE_NAME = billingdb)
   )
)
```

В настройках Data Source указать:  
Вкладка General:  
Name: что хочешь, например `market-billing-dev-tns`  
Connection Type: TNS  
TNSADMIN: путь к каталогу с файлом tnsnames.ora  
TNS name: `billingdev01.yandex.ru`  
User: `sysdev`  
Password: ... (пока спрашивай в чате)  

Вкладка Schemas:  
Schema pattern: `*:@,MARKET_BILLING,MBI_CORE,PUBLIC,SHOPS_WEB,WUSER`

Заполненная вкладка General выглядит так: [картинка](https://jing.yandex-team.ru/files/lena-san/market-billing-bd-idea-oracle-dev.png)

**Tip для Ubuntu:** Если в процессе подключения к БД у вас возникает ошибка(
``` IO Error: could not resolve the connect identifier "billingprod.yandex.ru" ```),  попробуйте заменить относительный путь к фалу ``` tnsnames.ora ``` на абсолютный путь от корня файловой системы.

#### Как проверить

В окне Database выбрать подключение к разработческой БД,
внутри выбрать схему `MARKET_BILLING`, внутри каталог `tables`
и дважды кликнуть на таблицу AGENCY.

Должна открыться вкладка с выборкой из этой таблицы.
Выглядит так: [картинка](https://jing.yandex-team.ru/files/lena-san/market-billing-db-agency.png)

Если так не происходит &mdash; надо разбираться.

### Oracle, Idea, тестовая БД


Файл tnsnames.ora:

```
BILLINGTEST01.YANDEX.RU =
   (DESCRIPTION =
            (ADDRESS_LIST =
              (ADDRESS = (PROTOCOL = TCP)(HOST = mdbaas-sas-scan.paysys.yandex.net)(PORT = 1521))
              (ADDRESS = (PROTOCOL = TCP)(HOST = mdbaas-vla-scan.paysys.yandex.net)(PORT = 1521))
            )
          (CONNECT_DATA =
        (SERVER = DEDICATED)
      (SERVICE_NAME = billingtst02)
   )
)
```

В настройках Data Source указать:  
Вкладка General:  
Name: что хочешь, например `market-billing-test-tns`  
Connection Type: `TNS`  
TNSADMIN: путь к каталогу с файлом tnsnames.ora  
TNS name: `billingtest01.yandex.ru`  
User: `market_billing`  
Password: ... (посмотреть в секрете <https://yav.yandex-team.ru/secret/sec-01d7kp1kt0074hfqcnqps7v8xp>, ключ `market_billing.billing.password`)

Вкладка Schemas:  
Schema pattern: `*:@,MARKET_BILLING,MBI_CORE,PUBLIC,SHOPS_WEB,WUSER`

### Oracle, Idea, продакшн БД

Файл tnsnames.ora:

```
billing.yandex.ru =
    (DESCRIPTION_LIST=
        (DESCRIPTION=
         (TRANSPORT_CONNECT_TIMEOUT=20)(RETRY_COUNT=5)
         (enable=broken)
         (ADDRESS_LIST=
             (LOAD_BALANCE=off)
                 (ADDRESS=(PROTOCOL=tcp)(HOST=csbilldb01f-vip.paysys.yandex.net)(PORT=1521))
                 (ADDRESS=(PROTOCOL=tcp)(HOST=csbilldb01v.paysys.yandex.net)(PORT=1521))
                 (ADDRESS=(PROTOCOL=tcp)(HOST=csbilldb01h-vip.paysys.yandex.net)(PORT=1521))
         )
         (CONNECT_DATA=
         (SERVICE_NAME=billingdb)
         (FAILOVER_MODE=(TYPE=SELECT)(METHOD=BASIC)(retries=3)(delay=5))
         )
        )
        (DESCRIPTION=
            (TRANSPORT_CONNECT_TIMEOUT=10)(RETRY_COUNT=2)
            (enable=broken)
            (ADDRESS_LIST=
                (LOAD_BALANCE=on)
                    (ADDRESS=(PROTOCOL=tcp)(HOST=csbilldb01f-vip.paysys.yandex.net)(PORT=1521))
                    (ADDRESS=(PROTOCOL=tcp)(HOST=csbilldb01v-vip.paysys.yandex.net)(PORT=1521))
                    (ADDRESS=(PROTOCOL=tcp)(HOST=csbilldb01h-vip.paysys.yandex.net)(PORT=1521))
            )
            (CONNECT_DATA=
            (SERVICE_NAME=billingdb-st)
            (FAILOVER_MODE=(TYPE=SELECT)(METHOD=BASIC)(retries=3)(delay=5))
            )
        )
    )
```

В настройках Data Source указать:  
Вкладка General:  
Name: что хочешь, например `market-billing-prod-tns`  
Connection Type: `TNS`  
TNSADMIN: путь к каталогу с файлом tnsnames.ora  
TNS name: `billing.yandex.ru`  
User: (твой доменный логин)  
Password: ... (особая процедура получения, см. ниже)

Вкладка Schemas:  
Schema pattern: `*:@,MARKET_BILLING,MBI_CORE,PUBLIC,SHOPS_WEB,WUSER`

Как получить пароль:
* переходите в систему [IDM](https://idm.yandex-team.ru)
* начинаете запрашивать роль (кнопка справа сверху)
* в качестве системы выбираете `БД Биллинга Маркета`. Автоматически подставится роль `права только на чтение`
* отправляете запрос
* когда роль подтвердят, на почту придет письмо с паролем для доступа к продакшен-Oracle

### Про работу с Oracle через sqlplus (cli-клиент) { #sqlplus }

Отдельная страница по установке: [{#T}](install-sqlplus.md)

Для подключения с использованием созданных ранее данных TNS нужно использовать следующую команду
```
TNS_ADMIN=__путь до конфига__ sqlplus user/password@host
```

например

```
TNS_ADMIN=~/market-billing-oracle/dev/ sqlplus sysdev/sysdev@BILLINGDEV01.YANDEX.RU
```


Полезное: использовать `rlwrap`, устанавливать переменную окружения `NLS_LANG=AMERICAN_AMERICA.WE8ISO8859P1`.

В клиенте делать:
```
set long 1000;
set pagesize 0;
```

### Postgres, psql, тестинг { #postgres-psql-testing }

`PGPASSWORD=<подставить пароль> psql -h c-mdbger39ogj8q5aagbjl.rw.db.yandex.net -p 6432 -U market_billing_testing`

Пароль брать из секрета <https://yav.yandex-team.ru/secret/sec-01f67mxn30447v0ec0yv8tjha0>
(открыть последнюю версию и скопировать значение из поля `market-billing-tms.postgresql.password`). Если секрет недоступен, то запросить роль разработчик в [ABC](https://abc.yandex-team.ru/services/market_billing).

Хостнейм всегда показывает на текущего мастера, см. подробнее в [{#T}](#postgres)


### Postgres, psql, продакшен { #postgres-psql-prod }

`PGPASSWORD=<подставить пароль> psql -h c-mdbke58al8r4k1jj1qn7.rw.db.yandex.net -p 6432 -U <твой доменный логин> -d market_billing`

Логин &mdash; доменный

Пароль брать из секрета, который прислали письмом от **mdb-admin@yandex-team.ru**, высылается при прорастании роли `DBaaS: market_billing / Чтение`, которая в свою очередь прорастает при добавлении в ABC группу разработки Биллинга Маркета
Обязательно указывать `-d market_billing` (для тестовой БД не требуется).

Хостнейм всегда показывает на текущего мастера, см. подробнее в [{#T}](#postgres)


### Postgres, Idea, тестинг { #postgres-idea-testing }

**Важно:** драйвер Postgres нужен версии 42.2.5 (окно с датасорсами, в левой панели вкладка Drivers)

Настройки Data Source:  
Вкладка General:  
Name: что хочешь, например `market-billing-tms-testing-url`  
Connection Type: URL only  
Authentication: User & Password  
User: `market_billing_testing`  
Password: (см. ниже)  
URL: `jdbc:postgresql://c-mdbger39ogj8q5aagbjl.rw.db.yandex.net:6432/market_billing_testing?prepareThreshold=0&preparedStatementCacheQueries=0&ssl=false`

Вкладка Schemas:  
Schema pattern: `@:@|market_billing_testing:market_billing,public,shops_web`

Пароль брать из секрета <https://yav.yandex-team.ru/secret/sec-01f67mxn30447v0ec0yv8tjha0>
(открыть последнюю версию и скопировать значение из поля `market-billing-tms.postgresql.password`)

Заполненная вкладка General выглядит так: [картинка](https://jing.yandex-team.ru/files/lena-san/market-billing-db-idea-postgres-testing.png)


### Postgres, Idea, продакшен { #postgres-idea-prod }

**Важно:** драйвер Postgres нужен версии 42.2.5 (окно с датасорсами, в левой панели вкладка Drivers)

Настройки Data Source:  
Вкладка General:  
Name: что хочешь, например `market-billing-tms-prod-url`  
Connection Type: URL only  
Authentication: User & Password  
User: `<твой доменный логин>`  
Password: (см. ниже)  
URL: `jdbc:postgresql://c-mdbke58al8r4k1jj1qn7.rw.db.yandex.net:6432/market_billing?prepareThreshold=0&preparedStatementCacheQueries=0&ssl=false`

Вкладка Schemas:  
Schema pattern: `@:@|market_billing_testing:market_billing,public,shops_web`

Пароль брать из секрета, который прислали письмом (**как стриггерить выдачу пароля для нового разработчика?**)

Заполненная вкладка General выглядит так: [картинка](https://jing.yandex-team.ru/files/lena-san/market-billing-db-idea-postgres-prod.png)


### Тарифница

**Важно:** драйвер Postgres нужен версии 42.2.5 (окно с датасорсами, в левой панели вкладка Drivers)

Настройки Data Source:  
Вкладка General:  
Name: что хочешь, например `тарифница prod/test/dev`  
Connection Type: URL only  
Authentication: User & Password  
User: `<login (см. ниже)>`  
Password: `<password (см. ниже)>`  
URL: `<url (см.ниже)>`  

| stand     | login                 | password                                                                                       | url                                                                                                                                                                                                                                                                                 | description                                                                                                                      |
|-----------|-----------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| `dev`     | `mbi_tariffs_dev`     | `mbi_tariffs_dev`                                                                              | `jdbc:postgresql://localhost:5432/mbi_tariffs_dev`                                                                                                                                                                                                                                  | Отдельной базы нет, поэтому создаем базу локально, накатываем запрос из файлика mbi-tariffs-service/src/liquibase/local/init.sql |
| `testing` | `mbi_tariffs_testing` | https://yav.yandex-team.ru/secret/sec-01ej6mrgg5p61fcfmjy0vyj3vd/explore/versions              | `jdbc:postgresql://man-ojfrkh1uby30exsr.db.yandex.net:6432,sas-1lkbul2079al7b9g.db.yandex.net:6432,vla-lq9y0aqw4vhhzqlq.db.yandex.net:6432/tpl_billing_testing?&targetServerType=master&ssl=true&sslmode=verify-full`                                                               | У этого пользователя есть W доступ                                                                                               |
| `prod`    | свой доменный логин   | должен прийти на почту, после того как запросить роль в idm: dbaas > mbi-tariffs-prod > чтение | `jdbc:postgresql://man-jrc0qxl4ahsq2wa9.db.yandex.net:6432,sas-htf7b3tgzmh31k7v.db.yandex.net:6432,vla-8pu9ao5hj5zx02gh.db.yandex.net:6432/mbi_tariffs_prod?sslmode=require&sslmode=require&targetServerType=preferSlave&loadBalanceHosts=true&prepareThreshold=0&connectTimeout=1` | R only                                                                                                                           |

#### W доступ
Если вдруг понадобился W доступ в прод, то можно посмотреть специально созданный для таких целей секрет [mbi-tariffs-duty](https://yav.yandex-team.ru/secret/sec-01f5dxb2034hhedwfn06tv849j/explore/versions) - тут и логин, и пароль и урл
Логин специальный, по нему есть (???) аудит




## Ссылки { #links }

* Специальный FQDN для текущего мастера в кластере Postgres: <https://docs.yandex-team.ru/cloud/managed-postgresql/operations/connect#fqdn-master>


# pers-notify
![статус сборки](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Abo_Pers_PersNotify/statusIcon)

## Разработка и релизы

### Ветки в git
#### develop

Текущая разработка. В ней должно содержаться то, что есть в мастере. Все новые фичевые ветки отцепляем от нее, 
мерджим в нее. Катаем в тестинг из нее.

#### master

Стабильная текущая ветка, в неё руками ничего не коммитим большого (кроме, может, мелких хотфиксов). При очередном
релизе в прод мерджим ветку develop в master, катаем.

### Локальная разработка

Для поднятия локального окружения требуется сделать некоторые шаги. 

Генерация проекта для IDEA происходит при помощи bash скрипта `/pers-notify/bin/idea.sh`, но для удобства можно создать симлинк в `~/bin` на этот скрипт:

`ln -s ~/arcadia/market/pers-notify/bin/idea.sh ~/bin/idea-pers`

Сгенерируем проект для IDEA, сохранив его в директорию `~/projects`:

`idea-pers` либо `~/arcadia/market/pers-notify/bin/idea.sh`

Необходимо иметь JDK11 для сборки проекта. Если он уже у вас имеется, то пропускаем этот шаг

1) Переходим в дирректорию `~/arcadia/jdk`
2) Выполняем команду ya make -DJDK_VERSION=11
3) Полученный архив разархивируем в удобное место (напр, `~/projects/JDK/JDK11`)

Настроим нужный SDK в настройках IDEA

1) Открываем проект `~/projects/pers-notify`
2) Добавим SDK (если отсутствует)
     + File-> Project Stricture -> SDKs -> Add JDK -> 
     + указать путь к загруженному в предыдущем шаге JDK `~/projects/JDK/JDK11`
3) Укажем необходимую SDK для проекта
     + File-> Project Stricture -> Project
     + В Project SDK указываем нашу подготовленную SDK для java 11
     + В Project language level указываем дефолтный SDK 11

#### Встроенные БД для автотестов

В автотестах используется два вида СУБД:

1. **Embedded MariaDB**: скачивается и запускается автоматически, не требует никаких ручных действий.
См. класс `EmbeddedMariaDatabaseBuilder` для подробностей.

2. **Embedded PostgreSQL** (только в тестах `market-utils`)

### Выкладка
#### Выкладка market-utils

Деплой происходит через [релизную машину](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/utils-stages)
или пайплайнами: 

* [В тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/lilucrm/release/new/market-utils-testing)
* [В продакшен из trunk](https://tsum.yandex-team.ru/pipe/projects/lilucrm/delivery-dashboard/market-utils-hotfix)

[Дашборд в Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_utils/) для тестинга и прода.

Собрать бинарники для Artifactory можно [тут](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_PersNotify_PersNotifyClient).

#### Выкладка market-mailer

Деплой происходит через [релизную машину](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/market-mailer)
или пайплайнами: 

* [В тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/lilucrm/release/new/market-mailer-testing)
* [В продакшен из trunk](https://tsum.yandex-team.ru/pipe/projects/lilucrm/delivery-dashboard/market-mailer-hotfix)

[Дашборд в Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_mailer/) для тестинга и прода.

### Запуск liquibase

Запуск команд liquibase осуществляется с помощью скрипта `/pers-notify/bin/liquibase-start.sh`.

Чтобы накатить изменения БД, необходимо выполнить следующую команду:

+ Для тестинга: `./liquibase-start.sh update test`
+ Для прода: `./liquibase-start.sh update prod`


### Описание

Компоненты уведомлений пользователей по email и push'ам.

[Страница на Wiki](https://wiki.yandex-team.ru/market/development/pers/notify/)

[Описание тестирования пушей](https://wiki.yandex-team.ru/market/development/pers/notify/push/test/)

### Адреса

Testing `market-utils.tst.vs.market.yandex.net:35826`
Production `market-utils.vs.market.yandex.net:35826`

[Api Reference (swagger)](http://market-utils.tst.vs.market.yandex.net:35826/api/swagger-ui.html)

### Мониторинги и графики

[Juggler market-mailer](https://juggler.yandex-team.ru/check_details/?host=market-mailer&service=market-mailer-dev)

[Grafana market-mailer](https://grafana.yandex-team.ru/dashboard/db/market-mailer?orgId=1)

[Juggler market-utils](https://juggler.yandex-team.ru/check_details/?host=market-utils&service=market-utils-dev)

[Grafana market-utils](https://grafana.yandex-team.ru/dashboard/db/market-utils?orgId=1)

[Golovan market-utils Nginx metrics](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketutils;ctype=production;prj=market)

[Balancer market-utils prod](https://grafana.yandex-team.ru/d/m3qTu4dmk/l3-vs-market-utils-vs-market-yandex-net?orgId=1)

[Balancer market-utils test](https://grafana.yandex-team.ru/d/000018227/l3-vs-market-utils-tst-vs-market-yandex-net?orgId=1)

[Описание мониторингов mailer](https://wiki.yandex-team.ru/users/a-danilov/Monitoringi-market-mailer/)

[Описание мониторингов utils](https://wiki.yandex-team.ru/users/apershukov/Monitoringi-market-utils/)

Запрос в CH: `select * from trace where target_module like 'market_utils' and environment='PRODUCTION' and date = ...`

#### Devel
Запуск на примере callisto и market-utils

1. `ssh callisto.yandex.ru "mkdir ~/dev/"`
2. `./gradlew --info uploadToDev -Pproject.upload.host=callisto.yandex.ru`
3. `ssh callisto.yandex.ru; cd ~/dev/market-utils/`
4. `./bin/market-utils-start.sh`

#### Testing

##### Market-Utils
[testing_market_utils_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_utils_vla/)

[testing_market_utils_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_utils_sas/)

##### Marker-Mailer
[testing_market_mailer_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_mailer_vla/)

[testing_market_mailer_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_mailer_sas/)

#### Production

##### Market-Utils
[production_market_utils_iva](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_utils_iva/)

[production_market_utils_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_utils_vla/)

[production_market_utils_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_utils_sas/)

##### Market-Mailer
[production_market_mailer_iva](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mailer_iva/)

[production_market_mailer_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mailer_vla/)

[production_market_mailer_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mailer_sas/)

### Подключение к продовой бд

#### Бд мейлера (MySql)

Переехали в mdb. Адреса в Yandex Cloud:

* [production](https://yc.yandex-team.ru/folders/foo0iertp0f42cdl1jqd/managed-mysql/cluster/mdbd5d5h00bi321nu9ec)
* [production tms](https://yc.yandex-team.ru/folders/foo0iertp0f42cdl1jqd/managed-mysql/cluster/mdbom1johrcp5a6fm7lp)
* [testing](https://yc.yandex-team.ru/folders/foo0iertp0f42cdl1jqd/managed-mysql/cluster/mdbgum2vihqhts89fu0m)
* [testing tms](https://yc.yandex-team.ru/folders/foo0iertp0f42cdl1jqd/managed-mysql/cluster/mdba61usf2kl5so7b5ob)

Адреса подключений:

- production: `jdbc:mysql://c-mdbd5d5h00bi321nu9ec.rw.db.yandex.net:3306/marketnotify?useSSL=true&verifyServerCertificate=false&autoReconnect=true&characterEncoding=utf8&connectTimeout=2000`
- testing: `jdbc:mysql://c-mdbgum2vihqhts89fu0m.rw.db.yandex.net:3306/marketnotify?useSSL=true&verifyServerCertificate=false&autoReconnect=true&characterEncoding=utf8&connectTimeout=2000`

Логин и пароль см. в репозитории [datasources-ng](https://github.yandex-team.ru/cs-admin/datasources-ng/blob/master/pers/etcd.yml) (запрашивайте права доступа, если репозиторий не виден).
Ключи:
- `market.utils.notify.url`
- `market.utils.notify.username`
- `market.utils.notify.password`

Графики по БД в соломоне:

* [production](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_mdbd5d5h00bi321nu9ec&service=mdb&host=*&graph=auto&stack=false&dc=by_host&hideNoData=true&l.sensor=*)
* [testing](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_mdbgum2vihqhts89fu0m&service=mdb&host=*&graph=auto&stack=false&dc=by_host&hideNoData=true&l.sensor=*)

### Разное

1. Временно остановить отправку сообщений EMAIL_SUBTYPE, запомнив время, когда было выключение
2. сделать необходимые изменения в шаблоне + задеплоить приложение! (если что-то менялось)
3. разрешить подтип
4. переотправить все письма соответствующего подтипа, которые зафейлились по причине выключения подтипа 
начиная с момента его выключения. Это удобно сделать с помощью хранимой в MySQL процедуры resend_all.
Чтобы ей воспользоваться, надо в таблицу TMP_RESEND вставить айдишники тех писем из EVENT_SOURCE,
которые надо переотправить (предварительно на всякий случай очистить TMP_RESEND).
Вставить их туда можно как раз с помощью запроса по критериям времени, подтипа и статуса, как писал выше.
Ну а потом уже выполнить процедуру - она создаст копии тех писем, айдишники которых в TMP_RESEND, в статусе NEW. 
И они в порядке очереди отправятся.
5. call resend_all()

#### Роботы
Робот мейлера для yt - robot-market-mailer

#### Профили

По умолчанию включен
-Dspring.profiles.active=$ENV_TYPE

development - дев-окружение (дев-сервер) 
testing - тестинг
production - прод

sender-testing - используется SenderTemplatesTest для подмены SenderClient 


### Задачи

Примеры [тут](TASKS.md)

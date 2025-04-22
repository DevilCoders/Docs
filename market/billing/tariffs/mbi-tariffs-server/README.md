Бекенд микросервиса тарифницы. Корневой тикет https://st.yandex-team.ru/MARKETMONEY-324

### Разработка
Разработка ведется в `arc`.

**N.B.** Серверная часть работает на JDK 17.

#### Где взять 17 jdk ?
Необходимо перейти по пути `cd ~/arcadia/jdks` и внутри выполнить команду `ya make -DJDK_VERSION=17`.
После успешного выполнения внутри этой папки появится `jdk17.tar`, который необходимо распаковать и сохранить к себе.

Собрать проект:
```bash
cd ~/arcadia/market/billing/tariffs
ya ide idea --group-modules=tree -r /full/path/to/folder/ --directory-based --iml-in-project-root -l --yt-store --stat --auto-exclude-symlinks
```

В проекте есть генерируемые ресурсы. На основе `openapi3.0` документации [генерируется](https://github.com/OpenAPITools/openapi-generator) интерфейсы и модели данных для контроллеров.
Все, что лежит в папке `generated` (подключается в процессе выполнения `ya make/ya ide idea`) трогать не стоит (потому что при следующей генерации там все потрется).
Поэтому, если надо что-то поменять в generated папке - менять надо в  [tariff-tech-api.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/tariffs/swagger/tariff-tech-api.yaml)

### Про базу
База представлена `PostgreSQL 10.15`. Чтобы запустить приложение на своей тачке, необходимо либо установить себе постгрес локально, либо поднимать его в докере, либо как вам угодно.
После установки, необходимо выполнить скрипт, который лежит по пути [src/liquibase/local/init.sql](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/liquibase/local/init.sql).
Затем, нужно накатить базу с помощью [liquibaseDev.sh](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/liquibaseDev.sh) (просто выполнив sh'ник)

Пример docker-compose.yml
```yml
version: '3.1'
services:
  postgres:
    image: postgres
    environment:
      # Переменные окружения для создания нужной базы, пользователя и его пароля соответственно.
      POSTGRES_DB:  mbi_tariffs_dev
      POSTGRES_USER:  mbi_tariffs_dev
      POSTGRES_PASSWORD:  mbi_tariffs_dev
    ports:
      # Можно указывать разные порты на хосте и мапить их контейнеру.
      # Дает возможность поднимать множество разных баз на хосте
      # Порт liquiabse и пропертей должен совпадать с указанным
      # Указывается в формате "порт_хоста:порт_контейнера"
      - 54321:5432
    volumes:
      # Если не хочется постоянно пересоздавать данные при перезапуске контейнера,
      # то можно замапить локальную директорию
      # Папка "data" должна существовать в директории где запускается compose
      - ./data:/var/lib/postgresql/data
```

Запускаем командой из папки с docker-compose.yml:
```bash
docker-compose up -d
```

"-d" означает что нужно запустить в виде демона.

На более свежих версиях докера команда выглядит так:
```bash
docker compose up -d
```

Если файл композа называется как-то по другому или лежит в другом месте, то его можно явно указать с помощью аргумента "-f":
```bash
docker-compose -f ./postgre.yml up -d
```

#### Прод
Чтобы ходить в **прод** базу, надо запросить роль в idm.
![](https://jing.yandex-team.ru/files/andreybystrov/Screenshot%20from%202021-05-13%2017-00-31.png)
```
Система -> DBaaS
Кластер -> mbi_tariffs_prod
Уровень доступа - чтение
```
После апрува роли, на почту придет логин/пароль, с которым можно сходить в базу.
Строка подключения jdbc: `jdbc:postgresql://mbi_tariffs_prod:PASSWORD@man-jrc0qxl4ahsq2wa9.db.yandex.net:6432,sas-htf7b3tgzmh31k7v.db.yandex.net:6432,vla-8pu9ao5hj5zx02gh.db.yandex.net:6432/mbi_tariffs_prod?sslmode=require&sslmode=require&targetServerType=preferSlave&loadBalanceHosts=true&prepareThreshold=0&connectTimeout=1`

#### Тестинг
В **тестинг** базу не надо запрашивать отдельно роль, посмотреть логин/пароль можно в [секретнице](https://yav.yandex-team.ru/secret/sec-01f5k0qnarwg9jj6n38htfm8fx/explore/versions)
Строчка подключения jdbc: `jdbc:postgresql://mbi_tariffs_testing:PASSWORD@man-pwxbj5hocutoi6pv.db.yandex.net:6432,sas-bll2l3dwyaim0re5.db.yandex.net:6432,vla-vwnsqi17ql0irf2s.db.yandex.net:6432/mbi_tariffs_testing?sslmode=require&sslmode=require&targetServerType=preferSlave&loadBalanceHosts=true&prepareThreshold=0&connectTimeout=1`

Так же бывает необходимость что-то поправить в тест/прод базе прям через insert/update.
Для этого существуют отдельные пользователи, которые имеют RW доступ в базы.
Использовать надо с осторожностью, прежде чем сделать `write` в базу, необходимо:
1. создать тикет в [очереди MARKETBILLING](https://st.yandex-team.ru/marketbilling)
2. призвать [Пашу](https://staff.yandex-team.ru/hmepas) и [Андрея](https://staff.yandex-team.ru/andreybystrov)
3. дождаться апрува изменений
4. после этого уже выполнять изменения

логины/пароли с `WRITE` доступом так же лежат в [секретнице](https://yav.yandex-team.ru/secret/sec-01f5dxb2034hhedwfn06tv849j/explore/versions) (обрати внимание на то, что там другой урл подключения)

### Локальный запуск
Создать конфигурацию:
```
Main class: ru.yandex.market.mbi.tariffs.MbiTariffs
Working dir: /full/path/to/folder/ #это та самая папка из команды выше
VM options:
-Djava.library.path=/home/andreybystrov/projects/works/mbi-tariffs/dlls
-Djna.library.path=/home/andreybystrov/projects/works/mbi-tariffs/dlls
-Denvironment=development
-Dlog4j2.contextSelector=org.apache.logging.log4j.core.async.AsyncLoggerContextSelector
-Dlog.dir=/tmp
-Dconfigs.path=/home/andreybystrov/arcadia/market/billing/tariffs/mbi-tariffs-server/src/main/properties.d
-Dlog4j.configurationFile=/home/andreybystrov/arcadia/market/billing/tariffs/mbi-tariffs-server/src/main/conf/local/log4j2-test.xml
-Dspring.profiles.active=development
--enable-preview
--add-opens java.base/java.lang=ALL-UNNAMED
```
(На маке полный путь начинается с /Users/andreybystrov/... , на убунте /home/andreybystrov/....)

**P.S.** в /home/andreybystrov/projects/works/mbi-tariffs/dlls лежат нативные либы, нужна только одна - `libticket_parser2_java`.
Как собрать/скачать эту .so написано [тут](https://wiki.yandex-team.ru/passport/tvm2/library/). Так же эта либа скачивается автоматически в папку, в которую генерируем проект `/full/path/to/folder/dlls`

В проекте используется поход в blackbox. В деве и тестинге можно не ходить в блекбокс,а передавать заголовки [UserLogin и UserUid](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/main/java/ru/yandex/market/mbi/tariffs/mvc/interceptor/BlackboxInterceptor.java?rev=eef4956870b5c1ff26e53e633e3c1d3d3d16e816#L90), откуда и будет забираться инфа про юзера.
Так же можно передать [волшебный хедер](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/main/java/ru/yandex/market/mbi/tariffs/mvc/interceptor/JavaSecInterceptor.java?rev=63db34c0668e27a3a3fc949f31869bc96415f17e#L36) с [волшебным значением](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/main/java/ru/yandex/market/mbi/tariffs/mvc/interceptor/JavaSecInterceptor.java?rev=63db34c0668e27a3a3fc949f31869bc96415f17e#L41), чтобы скипать проверки `javasec'a` (доступно везде, кроме прода)

Запрос для curl:
```bash
curl -k -X POST -H "Content-Type:application/json" -H "UserLogin:test" -H "UserUid:123" -d'[]' 'http://localhost:8080/tariffs/summary'
```

Jetty стартует на 8080 порту, переопределить можно так:
1. создать 00_local.properties по пути `src/main/properties.d/development`
2. прописать там:
```
http.port=8080 # порт для http запросов
tms.port=8083  # tms консолька
```

### Environments
- Testing    : https://billing-admin.tst.market.yandex.ru/
- Production : https://billing-admin.market.yandex.ru/

Хосты в няне:
- Testing : [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_tariffs_sas/) и [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_tariffs_vla/)
- Production : [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_tariffs_sas/) и [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_tariffs_vla/)

Релизная машина: https://tsum.yandex-team.ru/pipe/projects/mbi/delivery-dashboard/mbi-tariffs

Группа в abc : [Market Billing Tariffs](https://abc.yandex-team.ru/services/market_tariffs/)

Графики в графане: [Mbi tariffs](https://grafana.yandex-team.ru/d/vMc1oF1Mz/mbi-tariffs?orgId=1) (в разработке)


### FAQ
> ошибка вида "Caused by: java.io.FileNotFoundException: class path resource [<any files>] cannot be resolved to URL because it does not exist"

Правой кнопкой по модулю mbi-tariffs -> Rebuild (ну или build) module `mbi-tariffs`

> Как завести новую услугу?

Достаточно выполнить несколько шагов:
1. Добавить новый тип в ServiceTypeEnum (редактировать надо в [tariff-tech-api.yaml](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/swagger/tariff-tech-api.yaml))
2. Добавить новую jsonSchema, наследника от `CommonJsonSchema` (редактировать надо в [tariff-tech-api.yaml](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/swagger/tariff-tech-api.yaml))
3. Добавить новый мета конвертер, унаследовав от [AbstractMetaConverter](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/main/java/ru/yandex/market/mbi/tariffs/service/meta/converter/AbstractMetaConverter.java) и добавить в [MetaConverterService](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/main/java/ru/yandex/market/mbi/tariffs/service/meta/MetaConverterService.java)
4. Добавить новый fields supplier, унаследовав от [AbstractFieldsSupplier](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/main/java/ru/yandex/market/mbi/tariffs/service/meta/fields/AbstractFieldsSupplier.java) и добавить в [MetaFieldsService](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/main/java/ru/yandex/market/mbi/tariffs/service/meta/MetaFieldsService.java)
5. Поправить тест [SuggestsControllerTest#testGetEnumTypes](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/test/java/ru/yandex/market/mbi/tariffs/mvc/SuggestsControllerTest.java)
6. Добавить jsonSchema из п.2 в клиента тарифницы в класс [TariffClientMetaConverter](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-client/src/main/java/ru/yandex/market/mbi/tariffs/client/TariffClientMetaConverter.java)
7. Добавить новую мету в тест [MetaConverterServiceTest#testDeserialize](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/test/java/ru/yandex/market/mbi/tariffs/service/meta/MetaConverterServiceTest.java) и в тест [MetaConverterServiceTest#testDeserializeFailed](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-server/src/test/java/ru/yandex/market/mbi/tariffs/service/meta/MetaConverterServiceTest.java)

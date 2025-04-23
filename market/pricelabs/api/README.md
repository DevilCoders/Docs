# Описание проекта
Ручки, которыми можно управлять PriceLabs-ом (получать данные, устанавливать, планировать какие-то задачи).

Ручки описаны в модели **contract-first**, по формальному описанию [OpenAPI v3](https://swagger.io/specification/) 
генерируются интерфейсы Spring-а, которые затем реализуются.

Основное описание интерфейсов: [public-api.yaml](../core/src/main/resources/openapi/public-api.yaml)

Ручки доступны как:
 * тестинг - [https://pricelabs-api2.tst.vs.market.yandex.net](https://pricelabs-api2.tst.vs.market.yandex.net)
 * прод - [https://pricelabs-api2.vs.market.yandex.net](https://pricelabs-api2.vs.market.yandex.net)


# Детали реализации

## Аутентификация в ручках (TVM2)
Используем TVM2.
В проде аутентификация обязательна, **clientId = 2013474**. 

## Генерация ручек
Интерфейсы Spring генерируются автоматически при сборке приложения через **ya** (или при генерации проекта IDEA через
**ya ide idea**). Причем мы их помещаем в отдельный *source set* в модуле **core**, так что они доступны и **API**, 
и **TMS**. 

Генерация происходит в [openapi-get.inc](../core/openapi-gen.inc). Отдельная сборка и отдельный контракт [internal-api.yaml](../core/src/main/resources/openapi/internal-api.yaml) описывает ручки модуля **TMS**.  

Пример реализации ручек может посмотреть в классе [PublicAutostrategiesApi](src/main/java/ru/yandex/market/pricelabs/api/api/PublicAutostrategiesApi.java)

## Работа с YT
**markov** используется только для того, чтобы проверить, для какого кластера сейчас включена **sync** репликация (такой кластер считается *активным*, с консистентными данными).

После чего все запросы делаются в настоящие кластеры динтаблиц: **seneca-sas** или **seneca-vla**. Такое поведение допустимо, т.к. в настоящий момент все запросы являются запросами на чтение. Это может быть изменено в https://st.yandex-team.ru/PL-3586

Каждый процесс **API** выбирает активный кластер самостоятельно, см. [CanaryTableSwitch](src/main/java/ru/yandex/market/pricelabs/api/yt/CanaryTableSwitch.java).


## Работа с Clickhouse
Сделано как временное решение для служебных запросов (из поддержки), см. [PublicSupportApi](src/main/java/ru/yandex/market/pricelabs/api/api/PublicSupportApi.java).

## Работа с PostgreSQL
В настоящий момент выполняются только RO запросы, см. [BaseTasksServiceImpl](../core/src/main/java/ru/yandex/market/pricelabs/services/database/BaseTasksServiceImpl.java).

## На что обратить внимание

### Формат выдачи ручек, отличных от JSON
Ряд ручек поддерживает выдачу ответа в форматах **Excel** и **CSV**. Это ручки для отчетов, вызываемых из PLv1.
См. модули [csv](src/main/java/ru/yandex/market/pricelabs/api/spring/csv/OpenCsvHttpMessageConverter.java) и 
[excel](src/main/java/ru/yandex/market/pricelabs/api/spring/excel/ExcelHttpMessageConverter.java).

### Кэши
У нас есть in-memory кэш Spring-а: [CachedDataSource](src/main/java/ru/yandex/market/pricelabs/api/cache/CachedDataSource.java).

Кэш не синхронизирован с состоянием в БД и потенциально может показывать устаревшие на 5 минут данные.


### Взаимодействие с балансом
См. [BalanceServiceImpl](src/main/java/ru/yandex/market/pricelabs/api/services/balance/BalanceServiceImpl.java).


### Взаимодействие с модулем TMS
В настоящий момент все модифицирующие операции выполняются в модуле **TMS**. Поэтому такие операции снова
заворачиваются в вызов ручки, описанной в Reftofit-е [SharedServiceImpl](src/main/java/ru/yandex/market/pricelabs/api/services/tms/SharedServiceImpl.java).

Получается довольно муторно, должно решиться в https://st.yandex-team.ru/PL-4108


## Генерация проекта IDEA
[../tms/README.md](../tms/README.md)


## Запуск тестов
[../tms/README.md](../tms/README.md)


## Запуск приложения локально

### Сборка TVM2
[../tms/README.md](../tms/README.md)

### Запуск

[../tms/README.md](../tms/README.md)

Класс для запуска: `ru.yandex.market.pricelabs.api.Main`

VM Options:
```
-Denvironment=testing
-Dspring.profiles.active=development
-Dpricelabs.tms.url=http://localhost:8081
-Dconfigs.path=${ARC}/market/pricelabs/api/src/main/properties.d
-Dlocal.properties=${HOME}/secret/api/testing/secrets.properties
-Dlogging.config=${ARC}/market/pricelabs/api/src/test-medium/resources/log4j2-test.xml
-Djava.awt.headless=true
-Dserver.max-http-header-size=64000
-Xmx1g
-Dpricelabs.health-house.jdbc.sslMode=none
-Dpricelabs.health-house.jdbc.url=jdbc:clickhouse://clickhouse-public-testing.market.yandex.net:443
```

 * [Файл секретов `${HOME}/secret/api/testing/secrets.properties`](https://yav.yandex-team.ru/secret/sec-01efbp07yzx2chx0xsez9dzwh1/explore/versions)

Приложение поднимется по адресу http://localhost:8080
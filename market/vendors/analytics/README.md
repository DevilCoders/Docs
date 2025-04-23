##Бэкенд аналитической платформы маркета

### Компоненты
1. platform — лапки АПИ для фронта.
2. tms — запуск регулярных задач по расписанию

### Обновление зависимостей
1. `ya make`
2. `ya ide idea --iml-in-project-root -lr ~/IntellijIdeaProjects/analyticsPlatform .`

### Запуск тестов
1. `ya make -tt`

### Запуск тестов из идеи
##### LINUX
1. <a href="https://clickhouse.yandex/#quick-start">Установить кликхаус</a>
2. Запустить сервер кликхауса локально `sudo service clickhouse-server start`.
3. Накатить скрипт для создания таблиц:
```
cat ~/ark/market/vendors/analytics/core/src/liquibase/clickhouse/clickhouse.sql | clickhouse-client --multiquery
```

##### OSX
- В докере изменить лимит напамять (2гб дефолтных не всегда хватает, 5гб вроде ок)
- Запустить докер-образ:
```
docker run -d --name dev-server -p 8123:8123 --ulimit nofile=262144:262144 yandex/clickhouse-server
```
- Установить clickhouse-client:
```
docker run -it --rm --link dev-server:clickhouse-server yandex/clickhouse-client --host dev-server
```
- Добавить в `.bash_profile` alias:
```
alias clickhouse-client="docker run -i --rm --link dev-server:clickhouse-server yandex/clickhouse-client --host dev-server
```
alias отличается ключом `-i` от запуска, где указано `it`
- Накатить скрипт для создания таблиц:
```
cat ~/ark/arcadia/market/vendors/analytics/core/src/liquibase/clickhouse/clickhouse.sql | clickhouse-client --multiquery
```

# YARD

Сервис для управления двором на наших складах (в будущем ¯\_(ツ)_/¯). В текущем виде простейшая реализация системы электронной очереди.


## Локальный запуск

### Шаг 1: Поднять локально базу

Выполнить в dependency-stubs:
```
docker-compose up -d
```


**ATTENTION:** Если вы пользуетесь Арком, папка должна быть смонтирована с параметром --allow-other, иначе ни docker ни liquibase не стартуют


### Шаг 2: накатить liquibase миграции


#### Установка liquibase

Установить liquibase локально (не обязательно, можно использовать cli jar-ник из зависимостей проекта)

**Mac**: ``
brew install liquibase
``

**Ubuntu**:
``
sudo snap install liquibase --beta
``

#### Накатка миграций

Скопировать дефолтные проперти для liquibase
```
cp dependency-stubs/liquibase.properties.dist dependency-stubs/liquibase.properties
```

С помощью хелпер-скрипта накатить миграции.
```
dependency-stubs/liquibase.sh update
```


### Шаг 3: Запустить приложение

Поднять приложение локально можно через запуск main'а `FulfillmentYard` со следующими аргументами VM:
```
-Denvironment=local
-Dspring.profiles.active=local
-Dlog.dir=logs
-Dserver.port=<порт>
-Dconfigs.path=<локальный путь до properties.d>
```

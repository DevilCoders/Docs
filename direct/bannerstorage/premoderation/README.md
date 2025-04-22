# Premoderation
## Сервис премодерации креативов

[![Build Status](https://babylon.yandex-team.ru/jenkins/buildStatus/icon?job=premoderation-build)](https://babylon.yandex-team.ru/jenkins/job/premoderation-build/)

###

Веб-интерфейс: [premoderation.bannerstorage.yandex.ru](https://premoderation.bannerstorage.yandex.ru/)

### Описание сервиса

Сервис premoderation используется для предварительной модерации креативов, загруженных клиентами.
Сервис представляет из себя web-интерфейс, который используется командой модераторов. Модераторам предоставляется следующий функционал работы с загруженными креативами:

- просмотр креативов;
- модерация креативов: указание причин отклонения у составных частей креативов;
- просмотр/редактирование причин отклонения составных частей креативов;
- просмотр истории модерации креативов;
- просмотр/редактирование документов к креативам;
- просмотр статистики:
  + по модераторам;
  + по DSP;
  + по причинам отклонения;
  + по причинам отклонения + агенствам;

#### Краткий перечень ресурсов

- [исходный код] 
- джоба по сборке контейнера в Jenkins - [premoderation-build]
- логи сервиса пишутся в наш elasticsearch-сервис [melastic] в индексы `premoderation-nginx-*` и `premoderation-backend-*`

### Архитектура сервиса

В текущей реализации сервис представляет из себя java-приложение в Docker-контейнере, слушающее порт 8080 и  взаимодействующее с базой данных на MS SQL. Приложение занимается отрисовкой web-интерфейса и взаимодействием с базой данных в рамках описанного выше функционала.

**Общая схема сервиса:**

![alt tag](https://jing.yandex-team.ru/files/lawyard/Servis_premoderatsii.pdf_1_stranitsa_2016-03-29_11-28-28.png)

### Сборка Docker-образа

Сборка образа запускается вручную с помощью джобы [premoderation-build].
После успешной сборки полученный образ заливается во внутрияндексовый [docker registry].
Получить тег нового образа можно на странице билда - название билда автоматически изменяется на название тэга:

![alt tag](https://jing.yandex-team.ru/files/lawyard/premoderation-build_99_registry.yandex.netmediasellingpremoderation99-efd107b_registry.yandex.netmediasellingpremoderatio_2016-12-16_15-56-19.png)

Нюансы:
- каждый новый контейнер загружается в [docker registry] с двумя тэгами - `latest` и уникальным тегом, сгенерированным в ходе билда образа;
- старые образы не удаляются, их всегда можно выгрузить из [docker registry] по тэгу;

### Запуск контейнера в ручном режиме ###

**Команда запуска контейнера в ручном режиме:**
```sh
docker run -d \
-e "SENTRY_DSN=<sentry_dsn>" \
-e "WEBAPP_PATH=<webapp_path>" \
-e "HTTP_PORT=<http_port>" \
-e "STILLAGE_URL=<stillage_url>" \
-e "JDBC_URL=<jdbc_url>" \
-e "JDBC_USERNAME=<jdbc_username>" \
-e "JDBC_PASSWORD=<jdbc_password>" \
-e "DEPLOY_JDBC_USERNAME=<deploy_jdbc_username>" \
-e "DEPLOY_JDBC_PASSWORD=<deploy_jdbc_password>" \
-e "HTTP_SCHEME=<http_scheme>" \
-p :8080:8080 --name premoderation registry.yandex.net/mediaselling/premoderation
```

Параметры запуска:

|Параметр|Описание|Значение по умолчанию|
|--------|--------|---------------------|
|SENTRY_DSN|URL Sentry, в который будут логгироваться ошибки||
|WEBAPP_PATH|Путь до web каталога|/usr/lib/yandex/bannerstorage-premoderation/webapp|
|HTTP_PORT|Порт, на который привязывается веб сервер|8080|
|STILLAGE_URL|URL сервиса Stillage|https://bannerstorage-stillage.yandex.net|
|JDBC_URL|URL до базы данных в формате jdbc:jtds:sqlserver://ip:port/BannerStorage||
|JDBC_USERNAME|имя пользователя в базе данных||
|JDBC_PASSWORD|пароль пользователя в базе данных||
|DEPLOY_JDBC_USERNAME|имя пользователя в базе данных для накатки вербы||
|DEPLOY_JDBC_PASSWORD|пароль пользователя в базе данных для накатки вербы||
|HTTP_SCHEME|Схема, по которой будет редиректиться на Login.jsp. По умолчанию http, для прода https||


**docker-compose.yml**
```sh
premoderation:
   image: registry.yandex.net/mediaselling/premoderation
   environment:
          - SENTRY_DSN=<sentry_dsn>
          - STILLAGE_URL=<stillage_url>
          - JDBC_URL=<jdbc_url>
          - JDBC_USERNAME=<jdbc_username>
          - JDBC_PASSWORD=<jdbc_password>
          - DEPLOY_JDBC_USERNAME=<deploy_jdbc_username>
          - DEPLOY_JDBC_PASSWORD=<deploy_jdbc_password>
          - HTTP_SCHEME=<http_scheme>
   ports:
    - "8080:8080"
```

И запуск:
```sh
docker-compose -f docker-compose.yml up -d
```


### Тестирование сервиса


#### Деплой

Выкатка сервиса в тестах делается с помощью yadt, а именно - yadt_docker и базового класса [nginx_dependent]
Описание сервиса: [PreModerationDocker]

#### Тестирование 

Тестирование сервиса проводится косвенно - сервис деплоится в составе общего стенда в джобе  [bannerstorage-functional]. Здесь есть две проверки:

* автоматическая: проверка, что контейнер стартует вообще
* ручная: вход в интерфейс премодерации, которая выкачена на тестовый стенд

### Деплой в продакшен

Деплой в прод проходит аналогично другим docker-сервисам - с использованием [saltstack].


## Документация от старой версии


To build using Gradle execute

`./gradlew -PartifactVersion=<версия сборки, обязательно> clean build collect`

Configuration
====
To run on Linux just execute

`./start.sh`

To run locally using IntelliJ IDEA just place the config file in `premoderation-web/src/main/resources` directory
and create Application configuration targeting `ru.yandex.Application` class. Also you will have to copy
log4j configuration files from `resources/conf` to `resources` dir.


[исходный код]: <https://github.yandex-team.ru/MediaSelling/bannerstorage-premoderation>
[premoderation-build]: <https://babylon.yandex-team.ru/jenkins/job/premoderation-build/>
[bannerstorage-functional]: <https://babylon.yandex-team.ru/jenkins/search/?q=bannerstorage-functional>
[saltstack]: <https://github.yandex-team.ru/MediaSelling/salt#premoderation>
[PreModerationDocker]: <https://github.yandex-team.ru/QAMS/bannerstorage-ft/blob/master/bannerstorage/yadt/PreModerationDocker.py>
[nginx_dependent]: <https://github.yandex-team.ru/QAMS/YADT-docker/blob/master/yadt_docker/nginx_dependent.py>
[melastic]: <https://melastic.yandex-team.ru>
[docker registry]: <https://wiki.yandex-team.ru/Cocaine/docker-registry-distribution/>

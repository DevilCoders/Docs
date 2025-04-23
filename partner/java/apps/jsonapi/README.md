# JsonAPI

API Партнёрского Интерфейса

### Настройка IDE для разработки

Здесь и далее подразумевается, что в переменной окружения `ARCADIA` хранится путь до корня Аркадии.
Например, если Аркадия смонтирована в `~/arc/arcadia`, то можно выполнить
```
export ARCADIA=~/arc/arcadia
```

#### Создание проекта в IntelliJ Idea

```
cd $ARCADIA/partner/java
ya ide idea --project-root=<some-folder-outside-aradia> --local --directory-based --group-modules=tree --iml-in-project-root
```
Здесь `<some-folder-outside-aradia>` - это папка вне Аркадии, в которой вам удобно
хранить проект.

После выполнения команды можно открывать эту папку в Idea.

#### Конфигурация для тестов

Чтобы тесты модуля `jsonapi` запускались из Idea, нужно, чтобы на машине стоял docker,
и он мог скачать нужный образ с тестовой БД.

##### 1) Запросить доступ к Docker registry

Идем на https://idm.yandex-team.ru. Жмём `Request role`. Заполняем верхнее поле:
* System: `Docker-registry`
* Branch of roles: `Prefixes`
* Prefix pattern: `partners/`
* Role: `contributor`

Если своего портрета ниже не видим, нажимаем кнопку `Me` напротив поля Staff.

Жмём жёлтую кнопку Request. Далее ждём, пока кто-то из коллег одобрит роль,
а тем временем переходим к следующим пунктам.

##### 2) Установить Docker

https://docs.docker.com/engine/install/

##### 3) Авторизовать Docker в registry

Инструкция по авторизации здесь: https://wiki.yandex-team.ru/docker-registry/#authorization

После выполнения этих шагов и подтверждения роли коллегами тесты `jsonapi` должны запускаться успешно.

### Запуск на dev-partner2

##### 1) Убедиться, что есть доступ к dev-partner2

```
ssh dev-partner2.yandex.ru
```
Если доступа нет, обратиться к `zurom@` за его получением.

##### 1) Собрать приложение

На локальной машине:
```
cd $ARCADIA/partner/java/apps/jsonapi
ya make --target-platform=linux
```

##### 2) Скопировать приложение на удалённую машину

На локальной машине:
```
rsync -avh $ARCADIA/partner/java/apps/jsonapi/yandex-partner-java-jsonapi/* dev-partner2.yandex.ru:~/jsonapi/yandex-partner-java-jsonapi
rsync -avh $ARCADIA/partner/java/apps/jsonapi/jsonapi-dev.sh dev-partner2.yandex.ru:~/jsonapi
```
##### 3) Запустить приложение

На удалённой машине:
```
cd ~/jsonapi && ./jsonapi-dev.sh
```

##### 4) Проверяем, что приложение отвечает

На локальной машине:
```
curl http://dev-partner2.yandex.ru:8080/api/v1/users/current
```

В ответе должна быть ошибка 401.


### Удалённый дебаг

Чтобы подключиться к приложению дебаггером, подключаться к удалённой машине по SSH нужно так:
```
ssh -L 5005:localhost:5005 dev-partner2.yandex.ru
```

После этого можно в Idea использовать Run configuration типа Remote с дефолтными параметрами.





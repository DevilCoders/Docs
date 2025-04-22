# Карта сервисов

**Карта сервисов** - описание сервиса в yml формате, включая документацию, API, зависимости и т.д.

Все карты находятся в [services/maps](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps). Изменяются/добавляются через PR. Карты обычных сервисов должны находиться в корне.
Карты MySQL [type mysql/mdb_mysql](https://docs.yandex-team.ru/classifieds-infra/service-map#mdb_mysql) должны находиться в поддиректории [mysql](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/mysql).
Карты PostgreSQL [type mdb_postgresql](https://docs.yandex-team.ru/classifieds-infra/service-map#mdb_postgresql) должны находиться в поддиректории [postgresql](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/postgresql).

## Примеры

[Простой пример](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/grpc-echo.yml)

## Базовые поля

```yml
name:         grpc-echo
description:  grpc echo test service
type:         service
sox:          false
owners:
  - https://staff.yandex-team.ru/departments/yandex_personal_vertserv_infra
  - https://staff.yandex-team.ru/spooner
startrek:     VOID
design_doc:  'https://wiki.yandex-team.ru/...'
src:         'https://github.com/YandexClassifieds/admin-utils/tree/master/grpc-echo'
chat_duty: https://t.me/chat
```

### name
Имя сервиса и ключевое поле в карте. По нему строиться имя балансера, связывается манифест деплоя, имя nomad job, регистрация в consul, пишутся логи, связываются сервисы и так далее.

**Обязательно:**
- иметь короткое имя (до 24 символов) без дополнительных префиксов таких как `yandex-vertis` (Ограничение действует только на сервисы с `type:service`)
- lowcase
- в качестве разделителя использовать `-`
- иметь одинаковое имя сервиса и название файла с картой сервиса

### owners

Список групп или пользователей (ссылка на staff) - владельцев сервисов. Владелец отвечает за его разработку и/или эксплуатацию. В случае внешнего сервиса — кто является основным контактом.

Возможные значения:
- Группа со staff в формате `https://staff.yandex-team.ru/departments/<group_url>`
  (Например, `https://staff.yandex-team.ru/departments/yandex_personal_vertserv_infra`)
- Пользователь со staff в формате `https://staff.yandex-team.ru/<login>`
  (Например, `https://staff.yandex-team.ru/spooner`)
  Если не указана группа, то нужно указать как минимум двух пользователей

### startrek
Название очереди в startrek
Должен быть доступ от [робота](https://staff.yandex-team.ru/robot-vertis-shiva)

### description
Короткое описание сервиса

### design_doc
Ссылка на описание архитектуры сервиса

### src
Ссылка на исходники

- Не является обязательным для [type mysql/mdb_mysql](https://docs.yandex-team.ru/classifieds-infra/service-map#mdb_mysql)

### type

Тип сервиса.

##### service
Обычный сервис соовествующий [правилам](https://docs.yandex-team.ru/classifieds-infra/conventions/service)

*Значение по умолчанию*

##### batch
[Периодическая задача](https://docs.yandex-team.ru/classifieds-infra/deploy/specification/periodic)
##### external
Внешний сервис (т.е. разрабатывается не Вертикалями).

##### mdb_mysql
MySQL база данных в MDB

##### mdb_postgresql
PostgreSQL база данных в MDB

{% note warning %}

Для типов `mdb_mysql` и `mdb_postgresql` также необходимо указать поле mdb_cluster (см. ниже)

{% endnote %}

На этапе валидации проверяется, что кластер существует в MDB и соответствует имени, указанному в карте (с суффиксами `-test` и `-prod` для тестинга и прода соотв.)

##### conductor
Сервис, который живет в [кондукторе](https://c.yandex-team.ru).
На этапе валидации проверяется, что пакет действительно существует.

##### jenkins
Сервис, который живет в [jenkins](https://j.vertis.yandex-team.ru).
На этапе валидации проверяется, что сервис действительно существует.

### mdb_cluster
Описывает уникальные идентификаторы кластеров в MDB
Поля:
- `prod_id`
- `test_id`

Пример:
```yml
mdb_cluster:
  prod_id: mdb00000000000000000
  test_id: mdb11111111111111111
```

### sox
Признак, что на данный сервис распостраняются [требования sox](sox.md)

*Значение по умолчанию: false*

### pci_dss

Признак, что на данный сервис распространяются [контроли pci-dss](https://wiki.yandex-team.ru/verticals/pcidss/pci-dss/)

*Значение по умолчанию: false*

### chat_duty
Ссылка на дежурный чат сервиса

### language
Язык на котором написан сервис. Поддерживаются:
- Java
- Scala
- Go
- NodeJs
- Python
- Php
- C++

## provides (API)
Описание предоставляемого API

```yml
provides:
  - name: my-api
    protocol: grpc
    port: 1337
    description: echo
```

### name
Имя предоставляемого интерфейса.

Используется в имени балансера как:
`<service_name>-<provides_name>.vrts-slb.<layer>.vertis.yandex.net:80`
В данном случае в проде сервис будет доступен по адресу:
`grpc-echo-my-api.vrts-slb.prod.vertis.yandex.net:80`

**Обязательно:**
- иметь короткое имя до 24 символов
- lowcase
- в качестве разделителя использовать `-`
- не может быть `monitoring` или `owner`

### protocol
Протокол предоставляемого интерфейса.

Варианты:
- **http**
  - health check: ручка `/ping`, отвечающая кодом `200`
  - timeout: 120s
- **grpc**
  - Подходит как для обычного request/response, так и для stream.
  - timeout: 3600s
  - health check: [grpc health check](https://github.com/grpc/grpc/blob/master/doc/health-checking.md)
- **tcp**
  - health check: проверка доступности порта

### port
Порт на котором находится API

**Рекомендуется:**
- Передовать данный порт в манифесте деплоя как переменную окружения

### description
Короткое описание сервиса

### old_address_test

<font color='red'>**DEPRECATED:**</font> Имя старого балансера в тесте. Требуется полное доменное имя. Параметр для плавного переезда на новый деплой.

### old_address_prod

<font color='red'>**DEPRECATED:**</font> Имя старого балансера в проде. Требуется полное доменное имя. Параметр для плавного переезда на новый деплой.

## depends_on
Описание зависимостей. В данном блоке могут быть:
- вертикальные сервисы с API, например <font color='green'>нужна ссылка на пример</font>
- общие вертикальные сервисы, например kafka <font color='green'>нужна ссылка на пример</font>
- яндексовые сервисы, например LogBroker <font color='green'>нужна ссылка на пример</font>
- внешние сервисы, например YouTube <font color='green'>нужна ссылка на пример</font>
- базы данных <font color='green'>нужна ссылка на пример</font>

Для добавления зависимости должен быть получен approve на pull request с изменениями от владельца сервиса. В pr призывается руководитель owner-группы, но подойдет approve от любого члена группы или подгрупп.

```yml
depends_on:
  - service: service-name
    interface_name: api
    expected_rps:   10
    failure_reaction:
        missing:           fatal
        timeout:           severe
        unexpected_result: graceful
        errors:            fatal
```

### service
Путь до карты сервиса от которого зависит данный сервис. Относительный путь в `services/maps/`
(Например, `shiva` или `mysql/main`)

### interface_name
Имя интерфейса (поле `name` в блоке `provides`)

### expected_rps
Ожидаемая нагрузка (в RPS), которую создаст текущий сервис в production

### failure_reaction
Реакция на проблемы сервиса-зависимости

**Поля:**
- `missing` - сервиса нет (нет в service-discovery, dns не резолвится, нет открытого порта)
- `timeout` - сервис есть, но не отвечает, удерживая соединение, отваливается по таймайту
- `unexpected_result` - сервис отвечает, но содержимое ответов не соответствует спецификации
- `errors` - Сервис отвечает с ошибками (5xx)

**Значения:**
- `fatal` - сервис не переживает данную проблему
- `severe` - сервис переживает проблему, но частично деградирует
- `graceful` - сервис умеете переживать проблему и на его работу это не влияет

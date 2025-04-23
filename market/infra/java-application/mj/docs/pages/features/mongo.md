# Модуль Mongo

## Особенности
* В основе лежит `spring-boot-starter-data-mongodb`
* Добавлена [embedded база](https://github.com/flapdoodle-oss/de.flapdoodle.embed.mongo)
* Конфигурирование можно осуществлять через `service.yaml` в разделе [modules.mongo](../how_it_works/configuration/service_yaml.md#modules).
* В одном месте можно задать все необходимые настройки [для каждой среды](../how_it_works/configuration/environment.md).

## Конфигурирование в service.yaml
### modules.mongo
В этом разделе поддерживаются все проперти спринга, имеющие префикс `spring.data.mongodb`

Доступные проперти перечислены [здесь](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data.spring.data.mongodb.authentication-database)

```yaml
modules:
  mongo:
    database: mydb
    username: mongouser
    port: 27019
```

### modules.mongo.embedded
В этом разделе поддерживаются все проперти спринга, имеющие префикс `spring.mongodb.embedded`. Для активации `embedded` базы используйте проперти `modules.mongo.embedded.enabled`.

Доступные проперти перечислены [здесь](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data.spring.mongodb.embedded.features)

```yaml
modules:
  mongo:
    embedded:
      enabled: true
      replSetName: my-repl-set-name2
```

Таким образом, с учетом дефолтных настроек, финальная конфигурация может выглядеть примерно так:
```yaml
modules:
  mongo:
    env:
      local:
        embedded:
          enabled: true
```

Эта конфигурация приведет к следующему:
* В локальном окружении (`-Denvironment=local`) будет использоваться `embedded` Mongo.
* В `production`, `testing` и других средах (т.к. не задали отдельных конфигураций) будет создаваться подключение к полноценной Mongo.

{% note warning %}

  **Не забудьте задать параметры подключения!** 
  Например, добавьте в секретницу проперти `spring.data.mongodb.uri`, указав в нем URI для подключения
  в таком формате:
```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database.collection][?options]]
```
Подробности [здесь](https://mongodb.github.io/mongo-java-driver/3.7/javadoc/com/mongodb/MongoClientURI.html).

{% endnote %}

## Кастомизация
* Чтобы донастроить `MongoClient`, можно создать бин `MongoClientOptions`.

  Дефолтный MongoClientOptions:
  ```java
  MongoClientOptions.builder()
    .writeConcern(WriteConcern.MAJORITY)
    .readPreference(ReadPreference.primary())
    .sslEnabled(true)
    .build();
  ```
* В крайнем случае можно реализовать свой бин `MongoClient`. Тогда стартером `MongoClient` создаваться не будет. В таком случае лучше всего написать нам в [чат](https://t.me/joinchat/RImGNXqbohFkOTg6), сказать каких настроек не хватает и мы добавим.


## Стартер для сервисов без MJ
Стартер предназаначен для быстрого подключения **Mongo** в любой проект на **Spring Boot**

### Установка
Добавить в `ya.make` зависимость:
```
market/infra/java-application/spring-boot-starters/mongo-spring-boot-starter
```

### Конфигурирование
Все конфигурирование аналогично конфигурированию в [service.yaml](#Конфигурирование-в-service.yaml), только происходит в пропертях.

## Ваши предложения
  На данный момент стартер имеет базовый функционал и подготовлен для дальнейшего расширения. Если у вас есть предложения по добавлению новых функций - приходите к нам в [чат](https://t.me/joinchat/RImGNXqbohFkOTg6).

# Модуль Postgres
## Особенности
* Конфигурирование можно осуществлять через `service.yaml` в разделе [modules.postgres](../how_it_works/configuration/service_yaml.md#modules)
* В одном месте можно задать все необходимые настройки [для каждой среды](../how_it_works/configuration/environment.md).
* В основе лежит `spring-boot-starter-data-jdbc`
* **Datasource** поддерживает трассировку
* Мониторинг базы данных
* Добавлен **Liquibase**
* Добавлена embedded база данных [Zonky и initializer для тестов](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/zonky-pg-spring-initializer)
* Добавлена конфигурация для работы с [postgres_local](https://a.yandex-team.ru/arc/trunk/arcadia/antiadblock/postgres_local/README.md) (решает проблему [флапающих тестов](https://st.yandex-team.ru/MARKETDX-334/attachments/40082933))
* Добавлена конфигурация для динамического выбора источника данных, который для `readonly` транзакций умеет ходить в реплику. Про динамические источники данных [смотреть тут](https://www.baeldung.com/spring-abstract-routing-data-source). Наша реализация [ReadWriteRoutingDateSource.java тут](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/postgres-spring-boot-starter/src/main/java/datasources/ReadWriteRoutingDateSource.java).
* Поддерживается весь функционал, предоставляемый `spring-boot-starter-data-jdbc`. С возможностями можно ознакомиться [здесь](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.sql) или [здесь](https://docs.spring.io/spring-boot/docs/1.4.0.M1/reference/html/boot-features-sql.html#boot-features-configure-datasource).
* Для более сложных случаев можно задать свой `Datasource` через код. Тогда стартером `Datasource` создаваться не будет. 
* Шаблон ченджлог-файла для _Liquibase_ генерируется автоматически по дефолтному пути
  При первичной генерации проекта, в `src/main/resources/liquibase/db-changelog.xml`
* Генерируются заглушки для функциональных тестов. Эту функцию можно [отключить](generation_settings.md#Настройка-генерации-исходников).

{% note info %}

Советуем в сложных случаях обратиться к нам в [чат](https://t.me/joinchat/RImGNXqbohFkOTg6), чтобы мы могли либо подсказать решение с использованием имеющихся возможностей стартера, либо добавить поддержку для ситуаций, аналогичных вашей.

{% endnote %}

## Конфигурирование service.yaml
### Основные свойства
Большинство настроек можно произвести заданием параметров через `service.yaml`. Доступные проперти перечислены [здесь](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html). Наиболее часто используемые проперти: [Datasource properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data.spring.datasource.dbcp2), [Liquibase properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data-migration.spring.liquibase.change-log).

{% note info %}

Проперти с префиксом `spring.*` задаются в разделе `modules.postgres`. Например, хотим задать такие проперти:
```
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username: postgres
spring.datasource.password: postgres
```
В `service.yaml` это будет выглядеть так:
```yaml
modules:
  postgres:
    datasource:
      url: jdbc:postgresql://localhost:5432/postgres
      username: postgres
      password: postgres
```

{% endnote %}



### Свойства production базы данных
#### Настройки datasource
modules.postgres.datasource - в этом разделе поддерживаются все проперти спринга, имеющие префикс [spring.datasource]((https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data.spring.datasource.dbcp2)).
Пример:
```yaml
modules:
  postgres:
    datasource:
      url: jdbc:postgresql://localhost:5432/postgres
      username: postgres
      password: postgres
      hikari:
        connectionTimeout: 20000
        maximumPoolSize: 5
```

#### Настройки liquibase
modules.postgres.liquibase - в этом разделе поддерживаются все проперти спринга, имеющие префикс [spring.liquibase](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data-migration.spring.liquibase.change-log).
Пример:
```yaml
modules:
  postgres:
    liquibase:
      enabled: true
      changeLog: classpath:liquibase/db-changelog.xml
```

{% note info %}

По умолчанию для `production` базы `liquibase` отключен.

{% endnote %}

#### Динамический источник данных

Позволяет балансировать запросы по инстансам базы данных, и часть запросов автоматически направлять на доступные readOnly-реплики.

Как это работает: в приложении создаются два пула соединений к базе данных. В `write`-пуле все запросы идут к master-у БД, а в `read`-пуле выбирается наиболее подходящий инстанс БД. По умолчанию, выбирается инстанс с наименьшим временем пинга (не важно master или slave), при этом исключаются реплики отстающие более чем на 10 секунд. Пул автоматически выбирается в зависимости от параметров текущей транзакции. ReadOnly-транзакции (`@Transactional(readOnly = true)`) будут использовать пул `read`, а `write` будет использоваться во всех остальных случаях.

В качестве драйвера `postgresql` по умолчанию будет [library/java/ds/pgdriver](https://a.yandex-team.ru/arc_vcs/library/java/ds/pgdriver).

```yaml
modules:
  postgres:
    routing:
      enabled: true
```

Список всех доступных параметров можно увидеть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/spring-boot-starters/postgres-spring-boot-starter/src/main/resources/postgres-routing.properties)

Способ выбора инстанса БД для чтения может быть изменен в зависимости от потребностей вашего приложения. По умолчанию используется `targetServerType=any`, что подходит для приложений, которые незначительно модифицируют данные, но много читают. Если ваше приложение много модифицирует данные, то имеет смысл выбрать `targetServerType=preferSlave` или `targetServerType=slave`.

Дополнительно можна задавать максимальное отставание используемой реплики БД через параметр `maxReplicationLag`. Значение по умолчанию 10000 мс.

Параметр `loadBalanceHosts` отвечает за алгоритм выбора инстанса БД. По умолчанию выбирается инстанс с наименьшим временем пинга (скорее всего в том же ДЦ), но можно выбирать и рандомно.

```yaml
modules:
  postgres:
    routing:
      enabled: true
      read:
        data-source-properties:
          targetServerType: perferSlave
          maxReplicationLag: 10000
          loadBalanceHosts: false

```



### Свойства embedded базы данных
#### Включение embedded
`modules.postgres.embedded.enabled` - это _boolean_-параметр для переключения между `embedded` и `production` базой данных. По умолчанию используется `production` база данных.

{% note info %}

По умолчанию для `embedded` баз `liquibase` включен. Ченджлог по умолчанию должен находиться в `classpath:liquibase/db-changelog.xml`

{% endnote %}

#### Тип embedded
`modules.postgres.embedded.type` - тип embedded базы данных. Возможные значения: `zonky`, `recipe`. По умолчанию: `zonky`. Тип `recipe` это не совсем embedded база, скорее это конфигурация для работы с [postgres_local](https://a.yandex-team.ru/arc/trunk/arcadia/antiadblock/postgres_local/README.md), предназначенной для тестов. Используется обычный `HikariDataSource`, поэтому можно сконфигурировать через `modules.postgres.datasource.*` и `modules.postgres.datasource.hikari.*`

Пример:
```yaml
modules:
  postgres:
    embedded:
      enabled: true
      type: recipe
```

{% note info %}

Если задан тип `recipe`, то в `test/ya.make` автоматически добавляются настройки для работы с рецептом (через `INCLUDE(recipe.postgres.test.ya.make)` в файле `test.modules.ya.make`).

{% endnote %}

#### Настройки для zonky
`modules.postgres.embedded.zonky` - параметры для настройки Zonky.
В этом разделе можно указать:
```
pgStartupWaitMs
cleanDataDirectory
dataDirectoryPath
serverConfig.*
localeConfig.*
connectConfig.*
overrideWorkingDirectoryPath
port
errorRedirector
outputRedirector
```

{% note info %}

По умолчанию `Zonky` использует случайный порт. Но для `local` окружения удобно использовать фиксированный порт. Поэтому для локального окружения можно задать `modules.postgres.embedded.zonky.port=5454` (_Или любой другой порт_).
Тогда можно подключиться к embedded базе, например через _IntelliJ IDEA_, для отладки:
![](https://jing.yandex-team.ru/files/sid-hugo/image%20%2811%29.png)

{% endnote %}


### Мониторинг
По умолчанию включен. Изменить можно через `modules.postgres.monitoring.enabled`

### Дефолтные настройки
**Все эти настройки можно переопределить заданием своих собственных значений.**

{% cut "Production" %}
```yaml
modules:
  postgres:
    datasource:
      url: jdbc:postgresql://${postgresql.hosts}/${postgresql.database.name}
      username: ${postgresql.username}
      password: ${postgresql.password}
      type: com.zaxxer.hikari.HikariDataSource
      driver-class-name: org.postgresql.Driver

      hikari:
        maximum-pool-size: 10
        connection-test-query: SELECT 1
        data-source-properties:
          ssl: true
          sslmode: require
          targetServerType: master
          prepareThreshold: 0

    liquibase:
      enabled: false
      change-log: classpath:liquibase/db-changelog.xml
```
{% endcut %}

{% cut "Zonky" %}
```yaml
modules:
  postgres:
    liquibase:
      change-log: classpath:liquibase/db-changelog.xml

    embedded:
      zonky:
        error-redirector: INHERIT
        output-redirector: INHERIT
```
{% endcut %}

{% cut "Recipe (postgres_local)" %}
```yaml
modules:
  postgres:
    liquibase:
      change-log: classpath:liquibase/db-changelog.xml

    datasource:
      url: jdbc:postgresql://localhost:${PG_LOCAL_PORT}/${PG_LOCAL_DATABASE}
      username: ${PG_LOCAL_USER}
      password: ${PG_LOCAL_PASSWORD}
      type: com.zaxxer.hikari.HikariDataSource
      driver-class-name: org.postgresql.Driver

      hikari:
        maximumPoolSize: 10
        minimumIdle: 1
        isRegisterMbeans: false
        idleTimeout: 60000
        connectionTimeout: 60000
        connectionTestQuery: set statement_timeout to '600s';
```
{% endcut %}

{% cut "Динамический источник данных" %}
```yaml
modules:
  postgres:
    datasource:
      routing:
        #write datasource
        write:
          url: jdbc:pgcluster://${postgresql.hosts}/${postgresql.database.name}
          username: ${postgresql.username}
          password: ${postgresql.password}
          type: com.zaxxer.hikari.HikariDataSource
          driver-class-name: ru.yandex.ds.pgdriver.PGClusterDriver

          maximum-pool-size: 10
          connection-test-query: SELECT 1
          read-only: false
          data-source-properties.ssl: true
          data-source-properties:
            sslmode: require
            prepareThreshold: 0
            targetServerType: master

        #read datasource
        read:
          url: jdbc:pgcluster://${postgresql.hosts}/${postgresql.database.name}
          username: ${postgresql.username}
          password: ${postgresql.password}
          type: com.zaxxer.hikari.HikariDataSource
          driver-class-name: ru.yandex.ds.pgdriver.PGClusterDriver

          maximum-pool-size: 10
          connection-test-query: SELECT 1
          read-only: true
          data-source-properties:
            ssl: true
            sslmode: require
            prepareThreshold: 0
            targetServerType: any

    liquibase:
      enabled: false
      change-log: classpath:liquibase/db-changelog.xml
```

{% endcut %}

### Пример конфигурации
**Таким образом, с учетом [дефолтных настроек](#дефолтные-настройки), финальная конфигурация может выглядеть примерно так:**
```yaml
modules:
  postgres:
    env:
      local:
        embedded:
          enabled: true
          zonky:
            port: 5454
      functionalTest:
        embedded:
          enabled: true
      functionalTestRecipe:
        embedded:
          enabled: true
          type: recipe
```

* В локальном окружении (`-Denvironment=local`) будет embedded база Zonky c фиксированным портом 5454. При запуске, с помощью _Liquibase_ будет накатываться чейнджсет из `classpath:liquibase/db-changelog.xml`.
* При запуске тестов в среде `functionalTest` будет использоваться embedded база Zonky с рэндомным портом. Аналогично, будет работать _Liquibase_
* При запуске тестов в среде `functionalTestRecipe` (задать в `ya.make` переменную окружения `ENV(ENVIRONMENT=functionalTestRecipe)`) приложение будет сконфигурировано для работы с [postgres_local](https://a.yandex-team.ru/arc/trunk/arcadia/antiadblock/postgres_local/README.md). _Liquibase_, как обычно, накатит чейнджсет.
* В `production`, `testing` и других средах (_т.к. не задали отдельных конфигураций_) будут использоваться [дефолтные настройки](#дефолтные-настройки): `HikariDataSource`, настройки подключения будут подхватываться из секретницы, _Liquibase_ отключен.

## Тестирование
Для простоты тестирования базы данных можно свои тесты наследовать от `ru.yandex.market.javaframework.postgres.test.AbstractJdbcRecipeTest`. С помощью `@ContextConfiguration` можно передавать свои бизнесовые компоненты.

```java
@ContextConfiguration(classes = UserDao.class)
public class UserDaoTest extends AbstractJdbcRecipeTest {

    @Autowired
    private UserDao userDao;

    @Test
    public void simpleTest() {
        jdbcTemplate.execute("SELECT 1");
    }
    
    @Test
    @Sql({"/users.sql"})
    public void getUserNameTest() {
        Assertions.assertEquals("John", userDao.getNameById(1));
    }
}
```

### Запуск тестов с рецептом Postgres
На классы с тестами можно повесить аннотацию `@ActiveProfile("functionalTest")` или проперти `spring.profiles.active=functionalTest` подгрузить через `@TestPropertySource("/test.properties")`.
Тогда при запуске через идею, тесты будут использовать **Zonky**.  
Но при этом в `ya.make` для тестов автоматически прописывается `ENV(environment=functionalTestRecipe)`, то есть явным образом задается окружение.
Явное задание окружения имеет приоритет над заданием окружения через спринговые профили.
Поэтому при запуске тестов через `ya make -t` (а, соответственно, и в аркадии) они будут использовать уже **рецепт Postgres**, а не Zonky.

## Стартер
Предназаначен для быстрого подключения **Postgres** в любой проект на **Spring Boot**
### Установка
Добавить в `ya.make` зависимость:
```
market/infra/java-application/spring-boot-starters/postgres-spring-boot-starter
```

### Конфигурирование
#### Стандартные свойства
Большинство настроек можно произвести заданием параметров через `properties-файлы`. Доступные проперти перечислены [здесь](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html). Наиболее часто используемые проперти: [Datasource properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data.spring.datasource.dbcp2), [Liquibase properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.data-migration.spring.liquibase.change-log).

#### Дополнительные свойства
Помимо [стандартных пропертей](#стандартные-свойства), через проперти можно задать все дополнительные параметры, описанные [выше](#конфигурирование-service.yaml). Для этого использовать префикс `mj.*`:

- `mj.postgres.embedded.enabled` - аналогичен [modules.postgres.embedded.enabled](#включение-embedded)
- `mj.postgres.embedded.type` - аналогичен [modules.postgres.embedded.type](#тип-embedded). 
- `mj.zonky.*` - аналогичен [modules.postgres.embedded.zonky](#Настройки-для-zonky). Поддерживаемые параметры:
    ```
    mj.zonky.pgStartupWaitMs
    mj.zonky.cleanDataDirectory
    mj.zonky.dataDirectoryPath
    mj.zonky.serverConfig.*
    mj.zonky.localeConfig.*
    mj.zonky.connectConfig.*
    mj.zonky.overrideWorkingDirectoryPath
    mj.zonky.port
    mj.zonky.errorRedirector
    mj.zonky.outputRedirector
    ```
- `mj.postgres.datasource.routing.enabled` - аналогичен [modules.postgres.datasource.routing.enabled](#динамический-источник-данных).
  В динамическом источнике данных есть отдельный datasource  для записи и отдельный для чтения. Для изменени дефолтных настроек источника данных для чтения можно задать собственные проперти с префиксом `mj.postgres.datasource.routing.read.*` , а для записи - `mj.postgres.datasource.routing.write.*`.

#### Мониторинг
По умолчанию включен. Изменить значение можно через проперти: `mj.postgres.monitoring.enabled`.

#### Дефолтные проперти
**Все эти настройки можно переопределить заданием своих собственных значений.**

{% cut "Production" %}
```
spring.datasource.url=jdbc:postgresql://${postgresql.hosts}/${postgresql.database.name}
spring.datasource.username=${postgresql.username}
spring.datasource.password=${postgresql.password}
spring.datasource.type=com.zaxxer.hikari.HikariDataSource
spring.datasource.driver-class-name=org.postgresql.Driver

spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.connection-test-query=SELECT 1
spring.datasource.hikari.data-source-properties.ssl=true
spring.datasource.hikari.data-source-properties.sslmode=require
spring.datasource.hikari.data-source-properties.targetServerType=master
spring.datasource.hikari.data-source-properties.prepareThreshold=0

spring.liquibase.enabled=false
spring.liquibase.change-log=classpath:liquibase/db-changelog.xml

logging.level.com.zaxxer.hikari.HikariConfig=DEBUG
```
{% endcut %}

{% cut "Zonky" %}
```
spring.liquibase.change-log=classpath:liquibase/db-changelog.xml

mj.zonky.error-redirector=INHERIT
mj.zonky.output-redirector=INHERIT
```
{% endcut %}

{% cut "Recipe (postgres_local)" %}
```
spring.liquibase.change-log=classpath:liquibase/db-changelog.xml

spring.datasource.url=jdbc:postgresql://localhost:${PG_LOCAL_PORT}/${PG_LOCAL_DATABASE}
spring.datasource.username=${PG_LOCAL_USER}
spring.datasource.password=${PG_LOCAL_PASSWORD}
spring.datasource.type=com.zaxxer.hikari.HikariDataSource
spring.datasource.driver-class-name=org.postgresql.Driver

spring.datasource.hikari.maximumPoolSize=10
spring.datasource.hikari.minimumIdle=1
spring.datasource.hikari.isRegisterMbeans=false
spring.datasource.hikari.idleTimeout=60000
spring.datasource.hikari.connectionTimeout=60000
spring.datasource.hikari.connectionTestQuery=set statement_timeout to '600s';
```
{% endcut %}

{% cut "Динамический источник данных" %}
```
#write datasource
mj.postgres.datasource.routing.write.url=jdbc:pgcluster://${postgresql.hosts}/${postgresql.database.name}
mj.postgres.datasource.routing.write.username=${postgresql.username}
mj.postgres.datasource.routing.write.password=${postgresql.password}
mj.postgres.datasource.routing.write.type=com.zaxxer.hikari.HikariDataSource
mj.postgres.datasource.routing.write.driver-class-name=ru.yandex.ds.pgdriver.PGClusterDriver

mj.postgres.datasource.routing.write.maximum-pool-size=10
mj.postgres.datasource.routing.write.connection-test-query=SELECT 1
mj.postgres.datasource.routing.write.read-only=false
mj.postgres.datasource.routing.write.data-source-properties.ssl=true
mj.postgres.datasource.routing.write.data-source-properties.sslmode=require
mj.postgres.datasource.routing.write.data-source-properties.prepareThreshold=0
mj.postgres.datasource.routing.write.data-source-properties.targetServerType=master

#read datasource
mj.postgres.datasource.routing.read.url=jdbc:pgcluster://${postgresql.hosts}/${postgresql.database.name}
mj.postgres.datasource.routing.read.username=${postgresql.username}
mj.postgres.datasource.routing.read.password=${postgresql.password}
mj.postgres.datasource.routing.read.type=com.zaxxer.hikari.HikariDataSource
mj.postgres.datasource.routing.read.driver-class-name=ru.yandex.ds.pgdriver.PGClusterDriver

mj.postgres.datasource.routing.read.maximum-pool-size=10
mj.postgres.datasource.routing.read.connection-test-query=SELECT 1
mj.postgres.datasource.routing.read.read-only=true
mj.postgres.datasource.routing.read.data-source-properties.ssl=true
mj.postgres.datasource.routing.read.data-source-properties.sslmode=require
mj.postgres.datasource.routing.read.data-source-properties.prepareThreshold=0
mj.postgres.datasource.routing.read.data-source-properties.targetServerType=any

spring.liquibase.enabled=false
spring.liquibase.change-log=classpath:liquibase/db-changelog.xml

logging.level.com.zaxxer.hikari.HikariConfig=DEBUG
logging.level.ru.yandex.market.starter.postgres.datasources.ReadWriteRoutingDateSource=DEBUG
```

{% endcut %}

### Дополнительная настройка для работы с recipe
Добавить в `test/ya.make`
```
INCLUDE(${ARCADIA_ROOT}/antiadblock/postgres_local/recipe/postgresql_bin.inc)

USE_RECIPE(
antiadblock/postgres_local/recipe/recipe
)

DEPENDS(
antiadblock/postgres_local/recipe
)
```

## Куда присылать фидбек
На данный момент стартер имеет базовый функционал и подготовлен для дальнейшего расширения. Предложения по добавлению новых функций приветствуются - приходите к нам в [чат](https://t.me/joinchat/RImGNXqbohFkOTg6).

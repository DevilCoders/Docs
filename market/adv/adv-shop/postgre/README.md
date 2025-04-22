## Библиотека для подключения postgre к проекту

1. ```ru.yandex.market.adv.config.EmbeddedPostgresAutoconfiguration``` - автоконфигурация для подключения **embedded
   postgre** к проекту.
2. ```ru.yandex.market.adv.config.PostgresAutoconfiguration``` - автоконфигурация для подключения **postgre** к проекту.

## Подключение postgre

1. Добавить в ```ya.make``` файл ```INCLUDE(${ARCADIA_ROOT}/market/adv/inc/postgre.inc)``` или прописать следующие
   строчки:

```yamake
INCLUDE(${ARCADIA_ROOT}/market/adv/inc/dependency_management.inc)

PEERDIR(
    # Market
    market/jlibrary/request/request-utils
    market/jlibrary/request/datasource-trace

    # Common
    contrib/java/org/postgresql/postgresql
    contrib/java/org/liquibase/liquibase-core
)
```

2. Добавить в конфигурационные файлы **00_postgres.properties**. Заполнить его следующим образом:

```properties
#DataSource
spring.datasource.driverClassName=org.postgresql.Driver
spring.datasource.type=com.zaxxer.hikari.HikariDataSource
spring.datasource.url=jdbc:postgresql://${postgresql.hosts}/${postgresql.database.name}?ssl=true&sslmode=require&targetServerType=master&prepareThreshold=0
spring.datasource.username=${postgresql.username}
spring.datasource.password=${postgresql.password}
#Hikari
spring.datasource.hikari.maximumPoolSize=20
spring.datasource.hikari.minimumIdle=5
spring.datasource.hikari.connectionTestQuery=select 1
spring.datasource.hikari.registerMbeans=true
#Liquibase
spring.liquibase.enabled=false
```

3. Добавить в конфигурационные файлы **properties.d/production** и **properties.d/testing** ```postgresql.hosts``` -
   хосты, на которых располагается БД в YC через запятую с портом.
4. Добавить в продовые и тесинговые секреты:
    1. ```postgresql.username``` - логин, под которым нужно ходить в БД.
    2. ```postgresql.password``` - пароль от логина, под которым нужно ходить в БД.
    3. ```postgresql.database.name``` - название БД в YC.
5. Добавить новый Logger в файл **conf/log4j2.xml**:

```xml

<Logger name="com.zaxxer.hikari.pool.HikariPool" level="debug">
    <AppenderRef ref="MAIN"/>
    <AppenderRef ref="SENTRY" level="ERROR"/>
</Logger>
```

## Подключение spring-data-jdbc

Так как ORM под запретом и не очень хорошо справляются с высокой нагрузкой без долгого и кропотливого тюнинга,
рекомендую использовать **spring-data-jdbc**.

1. Добавить в ```ya.make``` файл ```INCLUDE(${ARCADIA_ROOT}/market/adv/inc/postgre.inc)``` или прописать следующие
   строчки:

```yamake
INCLUDE(${ARCADIA_ROOT}/market/adv/inc/dependency_management.inc)

PEERDIR(
    # Common
    contrib/java/javax/transaction/javax.transaction-api

    # Spring
    contrib/java/org/springframework/boot/spring-boot-starter-data-jdbc
)
```

2. Добавить в конфигурационный файл **00_postgres.properties**:

```properties
#Spring data
spring.data.jdbc.repositories.enabled=true
```

3. Добавить в код ```SpringDataJdbcConfiguration```:

```java
import java.util.List;

import javax.annotation.Nonnull;

import org.springframework.context.annotation.Configuration;
import org.springframework.data.jdbc.core.convert.JdbcCustomConversions;
import org.springframework.data.jdbc.repository.config.AbstractJdbcConfiguration;
import org.springframework.data.jdbc.repository.config.EnableJdbcRepositories;

@Configuration
//Путь до пакета, в котором нужно искать Repository для запросов в БД
@EnableJdbcRepositories("ru.yandex.market.adv.content.manager")
public class SpringDataJdbcConfiguration extends AbstractJdbcConfiguration {

    @Nonnull
    @Override
    public JdbcCustomConversions jdbcCustomConversions() {
        return new JdbcCustomConversions(
            List.of()
        );
    }
}
```

4. Для конвертации в jsonb можно
   использовать ```ru.yandex.market.adv.database.jdbc.converter.reading.AbstractPGObjectToJsonbReadingConverter```
   и ```ru.yandex.market.adv.database.jdbc.converter.writing.AbstractJsonbToPGobjectWritingConverter```.

## Подключение embedded postgre

Для тестов и локального запуска рекомендуется использовать embedded postgre и recipe postgre.

1. Добавить в ```ya.make``` файл ```INCLUDE(${ARCADIA_ROOT}/market/adv/inc/postgre.inc)``` или прописать следующие
   строчки:

```yamake

SET(EMBEDDED_PG_VERSION 13.4.0)

INCLUDE(${ARCADIA_ROOT}/antiadblock/postgres_local/recipe/postgresql_bin.inc)
INCLUDE(${ARCADIA_ROOT}/market/jlibrary/zonky-pg-spring-initializer/ya.dependency_management.inc)

USE_RECIPE(
    antiadblock/postgres_local/recipe/recipe
)

DEPENDS(
    antiadblock/postgres_local/recipe
)

PEERDIR(
    market/jlibrary/zonky-pg-spring-initializer
)

ENV(
    postgres.embedded.recipe=true
)
```

2. Прописать в настройках ```99_functional_application.properties``` и ```99_local-overrides.properties```:
    1. ```postgres.embedded.enabled=true``` - включение embedded postgre.
    2. ```postgres.embedded.port``` - порт на котором нужно запустить embedded postgre.
    3. ```postgres.embedded.liquibase.changelog``` - путь в classpath приложения, в котором лежит liquibase changelog
       для наката БД.

```properties
#Embedded postgres
postgres.embedded.enabled=true
postgres.embedded.port=44627
postgres.embedded.liquibase.changelog=liquibase/db-changelog.xml
```

3. Прописать в абстрактном наследнике для тестового класса следующий код:

```java

import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.TestPropertySource;

import ru.yandex.market.adv.config.EmbeddedPostgresAutoconfiguration;
import ru.yandex.market.adv.test.AbstractTest;
import ru.yandex.market.javaframework.main.config.SpringApplicationConfig;
import ru.yandex.market.mboc.common.utils.PGaaSZonkyInitializer;

@SpringBootTest(
    webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT,
    // Порядок крайне важен, иначе не будет работать
    classes = {
        EmbeddedPostgresAutoconfiguration.class,
        SpringApplicationConfig.class
    }
)
@ContextConfiguration(initializers = PGaaSZonkyInitializer.class)
@TestPropertySource(locations = "/99_functional_application.properties")
public abstract class AbstractContentManagerTest extends AbstractTest {
}
```

4. Написать тестовый класс с использованием **db-unit**:

```java

import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;

import ru.yandex.market.adv.content.manager.database.entity.moderation.ModerationTaskStatus;
import ru.yandex.market.common.test.db.DbUnitDataSet;

class ModerationTaskRepositoryTest extends AbstractContentManagerTest {

    @Autowired
    private ModerationTaskRepository moderationTaskRepository;

    @DisplayName("Результат по заданию на модерацию успешно обновился в БД.")
    @DbUnitDataSet(
        before = "ModerationTaskRepository/csv/" +
            "updateDataAndResultById_notNullDataAndResult_updateOneRow.before.csv",
        after = "ModerationTaskRepository/csv/" +
            "updateDataAndResultById_notNullDataAndResult_updateOneRow.after.csv"
    )
    @Test
    void updateDataAndResultById_notNullDataAndResult_updateOneRow() {
        Assertions.assertThat(
                moderationTaskRepository.updateStatusAndDataAndResultById(
                    423L,
                    "423_4123_5132_BUSINESS",
                    ModerationTaskStatus.MODERATED.name(),
                    getResultModerationTaskDataModel(),
                    true
                )
            )
            .isEqualTo(1L);
    }
}
```

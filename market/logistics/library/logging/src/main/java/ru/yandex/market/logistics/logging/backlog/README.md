## Структурированное логирование в формате backlog-tskv

Подробнее с **форматом** можно ознакомиться тут
https://wiki.yandex-team.ru/users/senz/back-log/

### Поддержка и принцип работы

Для log4j 2.x и logback реализованы **layout'ы** работающие по 
cледующему принципу. При добавлении такого layout'a к некому appender'у
перехваченное событие будет на выходе трансформировано в строку
вышеупомянтого формата,  при этом также будет задействован MDC (Mapped Diagnostic Context) slf4j.

Поддерживаемые уровни логирования (видимость зависит от уровня логгера):
- DEBUG
- TRACE
- WARN
- INFO
- ERROR

#### Примеры конфигураций

Зависимость в gradle подключается из яндексового репозитория 
```
…    
repositories {
    maven {
        url "http://artifactory.yandex.net/market"
    }
}
…
dependencies {
    compile("ru.yandex.market.logistics:logging:${loggingVersion}")
}
…
```

Для аркадии
```
PEERDIR(
    market/logistics/library/logging
)
```

#### Log4j
__log4j2.xml__
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="DEBUG" packages="ru.yandex.market.logistics.logging.appender.log4j, ru.yandex.market.logistics.logging.backlog">
    <Appenders>
        <RollingFile name="MAIN"
                     fileName="${sys:log.dir}/app.log"
                     filePattern="nopattern">
            <BackLogLayout />
            <NoopRollingStrategy />
            <RotationBasedTriggeringPolicy checkCachePeriod="1000"/>
        </RollingFile>
    </Appenders>
    <Loggers>
        <Root level="info">
            <AppenderRef ref="MAIN"/>
        </Root>
    </Loggers>
</Configuration>
```

Не забыть добавить путь "ru.yandex.market.logistics.logging.backlog" в атрибут packages в конфигурацию

#### Logback
__appender/backlog.xml__
```xml
<?xml version="1.0" encoding="UTF-8"?>
<included>
    <appender name="BACK_LOG" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOG_PATH}/market_logistic_gateway-backlog-tskv.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${LOG_PATH}/archive/market_logistic_gateway-backlog-tskv-%d{yyyy-MM-dd}.log.gz</fileNamePattern>
            <maxHistory>3</maxHistory>
        </rollingPolicy>
        <encoder class="ch.qos.logback.core.encoder.LayoutWrappingEncoder">
            <layout class="ru.yandex.market.logistics.logging.backlog.layout.logback.BackLogLayout" />
        </encoder>
    </appender>
</included>
```
**Важно** при использовании layout'ов задавать **отдельный логгер** с RollingFileAppender'ом под эти цели и использовать его как в примере ниже, таким образом в файле структурированнного лога будет только то, что залогировано средствами библиотеки **(appender для root логгера приведет к записи абсолютно всего логирования и всех исключений)**

#### Примеры структурированного логирования

##### Объявление логгера при помощи slf4j
```java
// Отдельный логгер backLogger с RollingFileAppender'ом c BackLogLayout'ом
private static final Logger BACK_LOG = LoggerFactory.getLogger("backLogger");
```

Ключевым для структурированного логирования является класс **BackLogWrapper**, при помощи которого вспомогательная метаинформация (code, requestId ...) упаковывается в MDC, и происходит вызов терминального метода для логирования. 

**Важно** помнить, что после вызова любого терминального метода содержимое MDC сбрасывается, то есть для каждого вызова **(строчки лога)** своя метаинформация 

##### Логирование информации и ошибки 
```java
BackLogWrapper backLogWrapper = BackLogWrapper.of(BACK_LOG);

backLogWrapper
    .withCode("some info code")
    .withEntities("entityName", entityValuesList)
    .withExtra("extraKey", "extraValue")
    .info("Some info message");

backLogWrapper
    .withCode("some error code")
    .withEntity("some entity name", "some entity value")
    .withTags("error")
    .error("Error occured", e);
```




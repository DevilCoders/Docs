## Библиотека для копирования данных из YT в YT и из YT в PG

1. ```ru.yandex.market.adv.data.sync.config.DataSyncAutoconfiguration``` - автоконфигурация.

## Подключение библиотеки в проект

Библиотека подключается в проект благодаря spring-boot-autoconfigure. Для того чтобы конфигурация начала
инициализироваться, необходимо чтобы в classpath были YtStaticClientFactory YtDynamicClientFactory.
Вся конфигурация передается через родительские файлы properties

См.
1. ```market/adv/adv-shop/yt```
1. ```market/adv/adv-shop/postgre```


## Логирование

Чтобы включить логирование запросов
воспользоваться [инструкцией](https://yt.yandex-team.ru/docs/best_practices/howtorunproduction#zaranee-podgotovtes-k-otladke)
или сделать следующие шаги.

1. Добавить зависимость ```contrib/java/org/apache/logging/log4j/log4j-slf4j-impl```

```yamake
PEERDIR(
    ...
    contrib/java/org/apache/logging/log4j/log4j-slf4j-impl
    ...
)

DEPENDENCY_MANAGEMENT(
    ...
    contrib/java/org/apache/logging/log4j/log4j-slf4j-impl/2.14.1
    ...
)
```

2. Добавить новый Appender в файл **conf/log4j2.xml**:

```xml

<RollingFile name="YT" fileName="${sys:log.dir}/${sys:app.name}-data-sync.log"
             filePattern="${sys:log.dir}/${sys:app.name}-data-sync.log.%d{yyyy-MM-dd}.gz">
    <PatternLayout pattern="[%d] [%t] %X{market-request-id} %m%n"/>
    <TimeBasedTriggeringPolicy interval="1"/>
    <DefaultRolloverStrategy>
        <Delete basePath="${sys:log.dir}" maxDepth="1">
            <IfFileName glob="${sys:app.name}-data-sync.log.*.gz"/>
            <IfLastModified age="21d"/>
        </Delete>
    </DefaultRolloverStrategy>
</RollingFile>
```

3. Добавить новые Logger в файл **conf/log4j2.xml**:

```xml

<Loggers>
    <Logger name="ru.yandex.market.adv.data.sync" level="debug">
        <AppenderRef ref="YT"/>
        <AppenderRef ref="SENTRY" level="ERROR"/>
    </Logger>
    <Logger name="ru.yandex.yt" level="debug">
        <AppenderRef ref="YT"/>
        <AppenderRef ref="SENTRY" level="ERROR"/>
    </Logger>
    <Logger name="ru.yandex.market.adv.data.sync" level="debug">
        <AppenderRef ref="SENTRY" level="ERROR"/>
    </Logger>
</Loggers>
```

## Тестирование приложения с использованием библиотеки

Чтобы написать функциональные тесты, необходимо сделать следующее:

1. Прописать в ```ya.make``` ```INCLUDE(${ARCADIA_ROOT}/market/adv/inc/yt_test.inc)``` или явно написать.

```yamake
IF(OS_LINUX)
    INCLUDE(${ARCADIA_ROOT}/mapreduce/yt/python/recipe/recipe.inc)

    SYSTEM_PROPERTIES(
        YT_TOKEN none
        YT_USERNAME root
    )
ENDIF()
```

2. Прописать в тестовых ```application.properties```:
    1. ```yt.{dynamic/static}.proxy=${YT_PROXY:zeno}```;
    2. ```yt.{dynamic/static}.username=${YT_USERNAME:${user.name}}```;
    3. ```yt.{dynamic/static}.token=${YT_TOKEN:file:~/.yt/token}```.
    4. ```yt.{dynamic/static}.module.source```.

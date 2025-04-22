## Библиотека для подключения клиента YT

1. ```ru.yandex.market.adv.config.YtDynamicClientAutoconfiguration``` - автоконфигурация подключения YT клиента для
   динамических таблиц.
2. ```ru.yandex.market.adv.config.YtStaticClientAutoconfiguration``` - автоконфигурация подключения YT клиента для
   статических таблиц.

## Подключение библиотеки в проект

Библиотека подключается в проект благодаря spring-boot-autoconfigure. Для того чтобы конфигурация начала
инициализироваться, необходимо указать четыре обязательные настройки: ```yt.{dynamic|static}.proxy```
, ```yt.{dynamic|static}.username```, ```yt.{dynamic|static}.token``` и ```yt.{dynamic|static}.module.source```
. ```{dynamic|static}``` - это выбор из двух: **static** - для статических таблиц, и **dynamic** - для динамических.
Весь перечень настроек проекта:

1. Общие:
    1. ```yt.{dynamic|static}.proxy``` - имя кластера YT, к которому отправляются запросы.
    2. ```yt.{dynamic|static}.username``` - имя пользователя.
    3. ```yt.{dynamic|static}.token``` - токен пользователя для доступа к данным.
    4. ```yt.{dynamic|static}.module.source```- модуль, из которого идут
       запросы. [Все модули](https://a.yandex-team.ru/arc_vcs/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java)
       для трассировки.
    5. ```yt.{dynamic|static}.retry.count```- количество раз, которые нужно попробовать повторно отправить запрос. По
       умолчанию ```3```.
    6. ```yt.{dynamic|static}.medium```- указание способа хранения данных (на HDD, SSD и т.д.). По умолчанию не задан.
    7. ```yt.{dynamic|static}.compression```- тип сжатия данных. Подробнее можно почитать
       в [документации](https://yt.yandex-team.ru/docs/description/common/compression#get_compression). По
       умолчанию ```None```.
2. Клиент для статических таблиц:
    1. ```yt.static.ping_timeout```- таймаут пинг запроса в секундах. По умолчанию ```5```.
3. Клиент для динамических таблиц:
    1. ```yt.dynamic.replicas```- список реплик через запятую. По умолчанию не задан.
    2. ```yt.dynamic.read_only```- доступность только на чтение. По умолчанию ```false```.
    3. ```yt.dynamic.execution_pool``` - пул для выполнения запросов. По умолчанию не задан.
    4. ```yt.dynamic.api_execution_pool``` - пул для выполнения api-запросов. По умолчанию не задан.
    5. ```yt.dynamic.retry.operations_timeout_sec``` - таймаут в секундах между повторными запросами. Если задан как 0
       или меньше, игнорируется. По умолчанию ```0```.
    6. ```yt.dynamic.retry.global_timeout_sec``` - глобальный таймаут на выполнения запроса в секундах. Должен быть
       больше 0. По умолчанию ```60```.

## Логирование

Чтобы включить логирование запросов в YT можно
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

<RollingFile name="YT" fileName="${sys:log.dir}/${sys:app.name}-yt.log"
             filePattern="${sys:log.dir}/${sys:app.name}-yt.log.%d{yyyy-MM-dd}.gz">
    <PatternLayout pattern="[%d] [%t] %X{market-request-id} %m%n"/>
    <TimeBasedTriggeringPolicy interval="1"/>
    <DefaultRolloverStrategy>
        <Delete basePath="${sys:log.dir}" maxDepth="1">
            <IfFileName glob="${sys:app.name}-yt.log.*.gz"/>
            <IfLastModified age="21d"/>
        </Delete>
    </DefaultRolloverStrategy>
</RollingFile>
```

3. Добавить новые Logger в файл **conf/log4j2.xml**:

```xml

<Loggers>
    <Logger name="ru.yandex.inside.yt" level="debug">
        <AppenderRef ref="YT"/>
        <AppenderRef ref="SENTRY" level="ERROR"/>
    </Logger>
    <Logger name="ru.yandex.yt" level="debug">
        <AppenderRef ref="YT"/>
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

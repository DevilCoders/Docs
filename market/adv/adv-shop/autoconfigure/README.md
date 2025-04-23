## Библиотека с базовыми автоматическими конфигурациями

1. ```ru.yandex.market.adv.config.CommonBeanAutoconfiguration``` - автоконфигурация для классов из библиотеки
   adv-shop/common
2. ```ru.yandex.market.adv.config.SchedulerAutoconfiguration``` - автоконфигурация для задач запускаемых по времени.
3. ```ru.yandex.market.adv.config.RequestLoggingFilterAutoconfiguration``` - автоконфигурация для логирования запросов в
   сервис и ошибок в sentry.
4. ```ru.yandex.market.adv.config.SolomonAutoconfiguration``` - автоконфигурация для pull-забора метрик solomon.

## Логирование запросов

1. Добавить новый Appender в файл **conf/log4j2.xml**:

```xml

<RollingFile name="REQUEST" fileName="${sys:log.dir}/${sys:app.name}-request.log"
             filePattern="${sys:log.dir}/${sys:app.name}-request.log.%d{yyyy-MM-dd}.gz">
    <PatternLayout pattern="[%d] [%t] %X{market-request-id} %m%n"/>
    <TimeBasedTriggeringPolicy interval="1"/>
    <DefaultRolloverStrategy>
        <Delete basePath="${sys:log.dir}" maxDepth="1">
            <IfFileName glob="${sys:app.name}-request.log.*.gz"/>
            <IfLastModified age="21d"/>
        </Delete>
    </DefaultRolloverStrategy>
</RollingFile>
```

2. Добавить новый Logger в файл **conf/log4j2.xml**:

```xml

<Logger name="ru.yandex.market.adv.filter.CommonsJsonRequestLoggingFilter" level="debug" additivity="false">
    <AppenderRef ref="REQUEST"/>
    <AppenderRef ref="SENTRY" level="ERROR"/>
</Logger>
```

3. Добавить новый Logger в файл **conf/local/log4j2.xml**:

```xml

<Logger name="ru.yandex.market.adv.filter.CommonsJsonRequestLoggingFilter" level="debug" additivity="false">
    <AppenderRef ref="CONSOLE"/>
</Logger>
```

## Настройки sentry

1. Создать проект в [Тестинге](https://sentry-test.market.yandex-team.ru/settings/sentry/projects/)
   и [Проде](https://sentry.market.yandex-team.ru/settings/sentry/projects/)
2. Добавить в конфигурационные файлы **properties.d/production** и **properties.d/testing** ```sentry.enable=true```.
3. Добавить в конфигурационные файлы **properties.d/production** и **properties.d/testing** ```sentry.dsn``` - ссылка на
   проект в Sentry ([После @](https://sentry.market.yandex-team.ru/settings/sentry/projects/adv-content-manager/keys/)).
4. Добавить в продовые и тесинговые секреты ```sentry.token``` - токен от проекта в
   Sentry ([До @](https://sentry.market.yandex-team.ru/settings/sentry/projects/adv-content-manager/keys/)).
5. Добавить в Appender в **conf/log4j2.xml**:

```xml

<Sentry name="SENTRY"/>
```

6. Добавить в каждый Logger в **conf/log4j2.xml**:

```xml

<AppenderRef ref="SENTRY" level="ERROR"/>
```

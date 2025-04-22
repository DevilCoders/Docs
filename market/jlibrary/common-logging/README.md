## Appender's логгеров

### Поддержка logrotate
Для logback и log4j 2.x релизованы триггеры и полтики с поддержкой внешней ротации для rolling
file appender.
Принцип следующий:
- triggering policy при записи нового события проверяет наличие файла лога по пути, и если таковой есть 
кеширует позитивный результат на некоторое время.
- если файл отсутствует - применяется noop rolling policy/strategy, которая просто создает новый
файл лога, отпуская старый дескриптор. Как сайдэффект, в переходный момент ротации в архивный файл могут попасть несколько секунд
новых логов.

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
    compile("ru.yandex.market:common-logging:${loggingVersion}")
}
…
```

Для аркадии
```
PEERDIR(
    market/jlibrary/common-logging
)
```

##### Logback
 
__appender/file.xml__
```xml
<?xml version="1.0" encoding="UTF-8"?>
<included>
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOG_PATH}/${LOG_FILE}.log</file>
        <rollingPolicy class="ru.yandex.market.common.logging.logback.NoopRollingPolicy" />
        <triggeringPolicy class="ru.yandex.market.common.logging.logback.RotationBasedTriggeringPolicy" />
        <encoder>
            <pattern>%date |%level| [%thread] [%logger{36}] - %replace(%msg){'[\r\n]+',' '} %replace(%ex{10}){'[\r\n]+', ' '}%nopex%n</pattern>
        </encoder>
    </appender>
</included>
```

##### Log4j
__log4j2.xml__
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="DEBUG" packages="ru.yandex.market.common.logging.log4j">
    <Appenders>
        <RollingFile name="MAIN"
                     fileName="${sys:log.dir}/app.log"
                     filePattern="nopattern">
            <PatternLayout pattern="${SIMPLE_LOG_PATTERN}"/>
            <NoopRollingStrategy />
            <RotationBasedTriggeringPolicy checkCachePeriod="1000"/>
        </RollingFile>
    </Appenders>
</Configuration>
```

**Важно!**
Не забудь добавить атрибут packages в конфигурацию, чтобы логгер смог найти плагин.
Значение filePattern неважно, тк в стратегии неиспользутся, но апендер считает поле обязательным. 

#### logrotate
```
/logs/app/*.log
/logs/app/*/*.log
{
    daily
    rotate 7
    compress
    dateext
    missingok

    # directory where to logs are archived
    olddir /logs/app/archive
    notifempty

    delaycompress

    # these directives are the default, but they're important, so let's be explicit!
    nocopytruncate
    nocreate
}
```

**Важно!** директива olddir должна указывать на папку с архивами логов, иначе logrotate будет ротировать и их, при текущем
glob правиле ротации. 

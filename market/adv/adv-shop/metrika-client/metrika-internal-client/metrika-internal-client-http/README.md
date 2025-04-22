## Подключение библиотеки в проект

Библиотека подключается в проект благодаря spring-boot-autoconfigure. Для того чтобы конфигурация начала
инициализироваться, необходимо указать две обязательные настройки: ```metrika.internal.client.http.url```
и ```metrika.internal.client.http.module.source```.

Весь перечень настроек проекта:

1```metrika.internal.client.http.url``` - сервер метрики, к которому отправляются запросы.

2```metrika.internal.client.http.module.source``` - модуль, из которого идут
   запросы. [Все модули](https://a.yandex-team.ru/arc_vcs/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java)
   для трассировки.

3```metrika.internal.client.http.tvm.serverId``` - tvm id сервера. Если не задано, запрос будет без tvm-токена.

4```metrika.internal.client.http.tvm.clientId``` - tvm id клиента (метрики). Если не задано, запрос будет без tvm-токена.

5```metrika.internal.client.http.tvm.secret``` - tvm секрет для создания токена. Если не задано, запрос будет без tvm-токена.

6```metrika.internal.client.http.retry.count``` - количество раз, которые нужно попробовать повторно отправить запрос. По
   умолчанию ```1```.
7```metrika.internal.client.http.timeout.connection``` - таймаут на соединение с сервисом в мс. По умолчанию ```5_000L```.

8```metrika.internal.client.http.timeout.read``` - таймаут на вычитывание данных в мс. По умолчанию ```20_000L```.

## Логирование
Клиент использует логгер с именем ```retrofit2.okHttpClientLoggingFilter.metrika.internal```
В приложении, которое использует этот клиент, определите логгер

```
    <Logger name="retrofit2.okHttpClientLoggingFilter.metrika.internal" level="debug" additivity="false">
        <AppenderRef ref="METRIKA.INTERNAL"/>
        <AppenderRef ref="SENTRY" level="ERROR"/>
    </Logger>
```

И настройте правила сохранения логов:
```
<RollingFile name="METRIKA.INTERNAL" fileName="${sys:log.dir}/${sys:app.name}-ok-http-metrika-internal.log"
             filePattern="${sys:log.dir}/${sys:app.name}-ok-http-metrika-internal.log.%d{yyyy-MM-dd}.gz">
    <PatternLayout pattern="[%d] [%t] %X{market-request-id} %m%n"/>
    <TimeBasedTriggeringPolicy interval="1"/>
    <DefaultRolloverStrategy>
        <Delete basePath="${sys:log.dir}" maxDepth="1">
            <IfFileName glob="${sys:app.name}-ok-http-metrika-internal.log.*.gz"/>
            <IfLastModified age="21d"/>
        </Delete>
    </DefaultRolloverStrategy>
</RollingFile>
```



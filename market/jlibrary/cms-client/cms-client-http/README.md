## Подключение библиотеки в проект

Библиотека подключается в проект благодаря spring-boot-autoconfigure. Для того чтобы конфигурация начала
инициализироваться, необходимо указать три обязательные настройки: ```cms.client.http.user```, ```cms.client.http.url```
и ```cms.client.http.module.source```. Весь перечень настроек проекта:

1. ```cms.client.http.user``` - идентификатор пользователя, от имени которого отправляется запрос.
2. ```cms.client.http.url``` - сервер CMS, к которому отправляются запросы.
3. ```cms.client.http.module.source``` - модуль, из которого идут
   запросы. [Все модули](https://a.yandex-team.ru/arc_vcs/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java)
   для трассировки.
4. ```cms.client.http.retry.count``` - количество раз, которые нужно попробовать повторно отправить запрос. По
   умолчанию ```1```.
5. ```cms.client.http.timeout.connection``` - таймаут на соединение с сервисом в мс. По умолчанию ```5_000L```.
6. ```cms.client.http.timeout.read``` - таймаут на вычитывание данных в мс. По умолчанию ```20_000L```.
7. ```cms.client.http.tvm.server_id``` - TVM идентификатор сервера. Если не задано, запрос будет без tvm-токена.
8. ```cms.client.http.tvm.client_id``` - TVM идентификатор клиента. Если не задано, запрос будет без tvm-токена.
9. ```cms.client.http.tvm.secret``` - TVM секрет для создания токена. Если не задано, запрос будет без tvm-токена.

## Тестирование приложения с использованием библиотеки

Чтобы написать функциональные тесты, необходимо просто использовать
библиотеку ```contrib/java/org/mock-server/mockserver-netty```.

## Логирование

Клиент использует логгер с именем ```retrofit2.okHttpClientLoggingFilter.cms```
В приложении, которое использует этот клиент, определите логгер

```
    <Logger name="retrofit2.okHttpClientLoggingFilter.cms" level="debug" additivity="false">
        <AppenderRef ref="CMS"/>
        <AppenderRef ref="SENTRY" level="ERROR"/>
    </Logger>
```

И настройте правила сохранения логов:

```
<RollingFile name="CMS" fileName="${sys:log.dir}/${sys:app.name}-ok-http-cms.log"
             filePattern="${sys:log.dir}/${sys:app.name}-ok-http-cms.log.%d{yyyy-MM-dd}.gz">
    <PatternLayout pattern="[%d] [%t] %X{market-request-id} %m%n"/>
    <TimeBasedTriggeringPolicy interval="1"/>
    <DefaultRolloverStrategy>
        <Delete basePath="${sys:log.dir}" maxDepth="1">
            <IfFileName glob="${sys:app.name}-ok-http-cms.log.*.gz"/>
            <IfLastModified age="21d"/>
        </Delete>
    </DefaultRolloverStrategy>
</RollingFile>
```

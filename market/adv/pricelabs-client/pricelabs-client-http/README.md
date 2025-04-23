## Подключение библиотеки в проект

Библиотека подключается в проект благодаря spring-boot-autoconfigure. Для того чтобы конфигурация начала
инициализироваться, необходимо указать три обязательные настройки: ```pricelabs.client.http.url```
и ```pricelabs.client.http.module.source```. Весь перечень настроек проекта:

2. ```pricelabs.client.http.url``` - сервер B2B Monetization, к которому отправляются запросы.
3. ```pricelabs.client.http.module.source``` - модуль, из которого идут
   запросы. [Все модули](https://a.yandex-team.ru/arc_vcs/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java)
   для трассировки.
4. ```pricelabs.client.http.retry.count``` - количество раз, которые нужно попробовать повторно отправить запрос. По
   умолчанию ```1```.
5. ```pricelabs.client.http.timeout.connection``` - таймаут на соединение с сервисом в мс. По умолчанию ```5_000L```.
6. ```pricelabs.client.http.timeout.read``` - таймаут на вычитывание данных в мс. По умолчанию ```20_000L```.

## Тестирование приложения с использованием библиотеки

Чтобы написать функциональные тесты, необходимо просто использовать
библиотеку ```contrib/java/org/mock-server/mockserver-netty```.

## Логирование
Клиент использует логгер с именем ```retrofit2.okHttpClientLoggingFilter.pricelabs.client```
В приложении, которое использует этот клиент, определите логгер

```
    <Logger name="retrofit2.okHttpClientLoggingFilter.pricelabs.client" level="debug" additivity="false">
        <AppenderRef ref="PL_CLIENT"/>
        <AppenderRef ref="SENTRY" level="ERROR"/>
    </Logger>
```

И настройте правила сохранения логов:
```
<RollingFile name="PL_CLIENT" fileName="${sys:log.dir}/${sys:app.name}-pricelabs-client.log"
             filePattern="${sys:log.dir}/${sys:app.name}-pricelabs-client.log.%d{yyyy-MM-dd}.gz">
    <PatternLayout pattern="[%d] [%t] %X{market-request-id} %m%n"/>
    <TimeBasedTriggeringPolicy interval="1"/>
    <DefaultRolloverStrategy>
        <Delete basePath="${sys:log.dir}" maxDepth="1">
            <IfFileName glob="${sys:app.name}-pricelabs-client.log.*.gz"/>
            <IfLastModified age="21d"/>
        </Delete>
    </DefaultRolloverStrategy>
</RollingFile>
```

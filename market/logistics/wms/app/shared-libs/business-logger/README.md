Библиотека позволяет писать в business-log<br/>
Топик логброкера: [market-wms@wms--business-log](https://logbroker.yandex-team.ru/logbroker/accounts/market-wms/wms/business-log) <br/>
Конфиг логшаттера для записи в облачный КХ: [market_wms_business_trace_mdb](https://health.market.yandex-team.ru/projects/*/logshatter/configs/market_wms_business_trace_mdb) <br/>
Для реализации в новом сервисе необходимо выполнить следующие действия:
1) Добавить в секцию `PEERDIR` `ya.make` зависимость `market/logistics/wms/app/shared-libs/business-logger`
2) В `resources/logback-appenders` добавить appender ([пример](https://a.yandex-team.ru/arc_vcs/market/logistics/wms/app/receiving/receiving-app/src/main/resources/logback-appenders/business-log.xml))
3) В `resources/logback-spring.xml` добавить настройки аппендера ([пример](https://a.yandex-team.ru/arc_vcs/market/logistics/wms/app/receiving/receiving-app/src/main/resources/logback-spring.xml)):
```
    <include resource="logback-appenders/business-log.xml"/>

    <logger name="business-log" level="DEBUG" additivity="false">
        <appender-ref ref="business-log" />
    </logger>
```
3) Убедиться, что в сервисе реализован бин `applicationModuleName`
4) В нужном месте заинжектить бин `BusinessLogger`
5) Добавить аналогичную другим сервисам конфигурацию в [конфиг-файл push-client для business-log](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/wms-push-client-config/etc/yandex/statbox-push-client/conf-enabled/market-wms-business-log.yaml)
6) Выкатить новые версии [wms-push-client-config](https://tsum.yandex-team.ru/pipe/projects/wms/delivery-dashboard/wms-push-client-config) и целевого сервиса

## Market-proto [![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_MarketProtoBuild/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_MarketProtoBuild)

Модуль _proto_ содержит файлы в формате protobuf: https://developers.google.com/protocol-buffers/

##### Как публиковать новые версии:
1. market-proto или market-proto-jetty9  
    - Публикация производится автоматически **pipeline-ом** в
     [ЦУМе](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-proto-java-library) 
    - И автоматически версии заливаются в **аркадию** в
        - [contrib/java/ru/yandex/market-proto](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/java/ru/yandex/market-proto)
        - [contrib/java/ru/yandex/market-proto-jetty9](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/java/ru/yandex/market-proto-jetty9)
    - Версия генерится по timestamp-у, ее можно посмотреть
    [в гитхабе](https://github.yandex-team.ru/market-java/market-proto/tags) 
    или [в артефактори](http://artifactory.yandex.net/yandex_market_releases/ru/yandex/market-proto/)
    - [Таска](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Tools_MarketProtoReleaseJetty9)
     публикует только _market-proto-jetty9_ и может использоваться если версия _market-proto-jetty9_ отстает от _market-proto_.

2. protobuf-handlers
    - Публикация _protobuf-handlers_ производится через
     [тимсити](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Tools_ProtobufHandlersRelease)
3. java-pbcat
    - Публикация _java-pbcat_ не производится. Эта тулза, которая устанавливается руками на машины разработчиков.  
    Подробнее: https://wiki.yandex-team.ru/market/mbo/descriptiondumpfiles/java-pbcat/

##### Публикация тестовых версий
Для публикации тестовой версии библиотеки можно использовать команду:  
``` ./gradlew -Pis_snapshot=true :market-proto-jetty9:release ```

### Логирование прото вызовов
ServiceClient и ServiceHandler могут логировать все исходящие и входящие прото запросы в лог файл.
Пример для клиента:
```
2019-05-06 00:00:15,909 TRACE [proto-client task-id-51929] Try #1. Send request: http://<HOST>:<PORT>/getLastTaskInfo?q={"item": [{"config_id": 8266,"return_all_states": true}]}
2019-05-06 00:00:15,922 TRACE [proto-client task-id-51929] Got result: {"status": {"status": "OK","message": ""},"task_info": [{"task_id": 12264,"config_id": 8266,"generated_requests_count": 7,"sended_requests_count": 7,"running_requests_count": 0,"received_responses_count": 0,"failed_requests_count": 7,"processed_requests_count": 0,"last_generate_time": 1553092574886,"last_send_to_hitman_time": 1553092588154,"hitman_job_url": "https://hitman.yandex-team.ru/r/jobs/51544300","state": "RUNNING_TASK","failed_processing_requests_count": 0,"generated_entities_count": 7,"cannot_requests_count": 0}]}
```
Пример для сервера:
```
2019-05-06 11:15:30,953 TRACE [proto-server AliasMakerServiceHandlerThread-3144] Method 'GetModels' called with json
2019-05-06 11:15:30,964 TRACE [proto-server AliasMakerServiceHandlerThread-3144] Method 'GetModels' finished, processing took 11 ms
2019-05-06 11:15:30,964 TRACE [proto-server AliasMakerServiceHandlerThread-3144] Method 'GetModels' result: {"model": [{"id": 441304846,"category_id": 396901,"vendor_id": 10814248, ......
```

Для того, чтобы настроить логирование нужно добавить в log4j2.xml следующие настройки:
```xml
<RollingFile name="PROTO" fileName="${sys:log.dir}/<SERVICE-NAME>-proto.log"
             filePattern="${sys:log.dir}/<SERVICE-NAME>-proto-%i.log.gz">
    <PatternLayout pattern="%d %-5p [%c{1} %t] %m%n"/>
    <SizeBasedTriggeringPolicy size="250 MB"/>
    <DefaultRolloverStrategy max="10"/>
</RollingFile>
<Async name="PROTO_ASYNC">
    <AppenderRef ref="PROTO"/>
</Async>

.....

<Logger name="proto-client" level="trace" additivity="false">
    <AppenderRef ref="PROTO_ASYNC"/>
</Logger>
<Logger name="proto-server" level="trace" additivity="false">
    <AppenderRef ref="PROTO_ASYNC"/>
</Logger>
```

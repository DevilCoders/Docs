[[toc]]


## About
Сервис хранит и выдает карточные дорожные события (камеры, дорожные работы, аварии, перекрытия, разведенные мосты, разговорчики), а так же комментарии и голоса (votes) к ним. [Fastcgi yacare](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/yacare) сервис, сидящий за nginx. Сервис развернут в RTC, база данных MongoDB развернута в Yandex.Cloud MDB.


## General information
| Key | Value |
|---|---|
| ABC | [maps-core-jams-infopoints](https://abc.yandex-team.ru/services/maps-core-jams-infopoints/) |
| Ответственные разработчики | [Разработчики maps-core-jams-infopoints](https://abc.yandex-team.ru/services/maps-core-jams-infopoints/?scope=development), в первую очередь [Игорь Ретинский](https://staff.yandex-team.ru/retinskii), [Александр Наплавков](https://staff.yandex-team.ru/twisterok) |
| Отвественные SRE | Игорь Ретинский (retinskii@yandex-team.ru) |
| Исходники | [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint) |
| XML schemas | [schemas](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymaps/infopoints/1.x) (сам infopoint НЕ проверяет xml документы на соответствие схемам) |
| protobuf | [road\_events](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/road_events) |
| Sedem | [sedem\_config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/sedem_config) |


## Instances
| Environment | URL |
|---|---|
| stable | [maps\_core\_jams\_infopoints\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_stable/) |
| prestable | [maps\_core\_jams\_infopoints\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_prestable/) |
| testing | [maps\_core\_jams\_infopoints\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_testing/) |
| load | [maps\_core\_jams\_infopoints\_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_load/) |
| unstable | [maps\_core\_jams\_infopoints\_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_unstable/) |


## Graphics
| Key | URL |
|---|---|
| stable (incl. prestable) | [maps-core-jams-infopoints-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-jams-infopoints-stable-panel-main/) |
| testing | [maps-core-jams-infopoints-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-jams-infopoints-testing-panel-main/) |
| load | [maps-core-jams-infopoints-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-jams-infopoints-load-panel-main/) |
| road events & comments (stable) | [maps-core-jams-infopoints-stable-moderation](https://yasm.yandex-team.ru/panel/twisterok._U04h7D/) |
| road events & comments (testing) | [maps-core-jams-infopoints-testing-moderation](https://yasm.yandex-team.ru/panel/twisterok._uqIfGv/) |
| road events & comments (load) | [maps-core-jams-infopoints-load-moderation](https://yasm.yandex-team.ru/panel/twisterok._jQzCkb/) |
| ratelimiter | [infopoint-ratelimiter2-panel](https://yasm.yandex-team.ru/template/panel/infopoint-ratelimiter2-panel/) |


## Monitorings (Juggler)
| Staging |  URL |
| --- | --- |
| stable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_stable%7Chost%3Dyt-account-maps-jams-infopoints-events-log%7Chost%3Dyt-pool-logfeller-maps-infopoints%7Chost%3Dlogbroker-maps-core-jams-infopoints&view=tiles) |
| prestable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_prestable) |
| testing | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_testing%7Chost%3Dyt-account-maps-jams-infopoints-events-log-testing&view=tiles) |
| load | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_load) |
| unstable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_unstable) |

## Monitorings (Solomon)

Для мониторинга потребления YT ресурсов, были добавлены алерты solomon, которые агрегируются Juggler-ом

### Solomon alerts
| Staging | URL |
| --- | --- |
| stable | [solomon](https://solomon.yandex-team.ru/admin/projects/maps-core-jams-infopoints/alerts) |
| testing | [solomon](https://solomon.yandex-team.ru/admin/projects/maps-core-jams-infopoints-testing/alerts) |

### Juggler aggregates
| Staging | URL |
| --- | --- |
| stable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dyt-account-maps-jams-infopoints-events-log%7Chost%3Dyt-pool-logfeller-maps-infopoints&view=tiles) |
| testing | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dyt-account-maps-jams-infopoints-events-log-testing&view=tiles) |

### Statistics alerts from daily_stat

| Staging | URL | Scheduler |
| --- | --- | --- |
| testing | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dsandbox.maps_core_jams_infopoints.daily_stat_testing&view=tiles) | [Sandbox](https://sandbox.yandex-team.ru/scheduler/24464/view) |
| stable | [juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dsandbox.maps_core_jams_infopoints.daily_stat_stable&view=tiles) | [Sandbox](https://sandbox.yandex-team.ru/scheduler/24463/view) |


## Database
[Документация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/database/readme.md)


## What happens when service is down
Слой дорожных событий и маршрутизатор используют последние дорожные события, которые удалось выгрузить. Невозможно добавить новые дорожные события, комментарий или проголосовать за дорожное событие. Невозможно посмотреть детальную информацию о дорожных событиях (включая комментарии). Невозможно модерировать (изменить/удалить) дорожные события. Может отсутствовать информация о разведении мостов и перекрытиях в зависимости от времени и продолжительности недоступности сервиса, таким образом, строимые маршрутизатором маршруты могут быть невалидными.


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/\* |
| Infopoints yacare service | /var/log/yandex/maps/infopoint/infopoint.log\* |
| Events log tskv | /var/log/yandex/maps/infopoint/infopoint-events-tskv.log\* |
| Shown events log tskv | /var/log/yandex/maps/infopoint/infopoint-shown-events-tskv.log\* |
| Iss log tskv | /var/log/yandex/maps/infopoint/infopoint-iss-tskv.log\* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/\* |
| Syslog (unfiltered) | /var/log/syslog |
| YT | ```SELECT * FROM hahn.`//logs/maps-log/1d/{date}` WHERE vhost = 'infopoints.maps.yandex.net' LIMIT 100;``` |
| Old mongodb oplog testing (YT) | [oplog](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/infopoint/oplog) |
| Old mongodb oplog stable (YT) | [oplog](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/infopoint/oplog) |
| tie-events | /var/log/yandex/maps/infopoint/tie-events-and-upload.log* |


## Shown Events Log
В лог `/var/log/yandex/maps/infopoint/infopoint-shown-events-tskv.log` записываются добавление/обновление/удаление точек, комментариев и голосования, которые мы показываем в Картах, то есть данные прошедшие модерацию. Этот лог потом используется для выгрузки данных в рамках takeout.

Поля:<br>
`key` - id агрегированной точки<br>
`timestamp` - время, когда событие произошло (unix time)<br>
`user` - инициатор действия<br>
`author` - автор сущности, над которой выполняется действие<br>
`client_ip` - ip-адрес, с которого поступил запрос на выполнение действия<br>
`client_port` - порт, с которого поступил запрос на выполнение действия<br>
`operation_type` - тип операции, список логируемых операций см. [в коде](https://a.yandex-team.ru/arc_vcs/maps/infopoint/lib/event_logger/logger.cpp)<br>
`value` - содержимое отправляемого события, json структура, содержимое которой зависит от `operation_type`, см. [код](https://a.yandex-team.ru/arc_vcs/maps/infopoint/lib/event_logger/logger.cpp).

## Events Log
Аналогично `Shown events log`-у ведется отдельное логирование для тех же ручек в отдельные YT таблицы.
Запись производится в `/var/log/yandex/maps/infopoint/infopoint-events-tskv.log` в формате tskv.
У данного лога нет никаких фильтров, т.е. все логируется как есть и хранится недолго.
Данный лог предназначен для сбора статистики.<br>
Помимо полей из `shown events log`'а также логирует:<br>
`uuid` - uuid пользователя-инициатора запроса<br>
`miid` - miid пользователя-инициатора запроса<br>

## Отправка в YT
Отправка в YT производится с помощью схемы.
`PushClient -> LogBroker -> Logfeller -> YT`.<br>
[Документация](https://wiki.yandex-team.ru/logfeller/connection/)

### Где лежат логи в YT
| log | staging | topic |
| --- | --- | --- |
| Events log | stable | [//home/logfeller/logs/maps-core-jams-infopoints-stable-events-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-infopoints-stable-events-log)|
| Events log | testing | [//home/logfeller/logs/maps-core-jams-infopoints-testing-events-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-infopoints-testing-events-log)|
| Shown events log | stable | [//home/logfeller/logs/maps-core-jams-infopoints-stable-shown-events-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-infopoints-stable-shown-events-log)|
| Shown events log | testing | [//home/logfeller/logs/maps-core-jams-infopoints-testing-shown-events-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-infopoints-testing-shown-events-log)|

### Статистика по Events log
По данным из таблиц [events-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-infopoints-stable-events-log) собирается статистика для последующего анализа

| Статистика | Ссылка |
| --- | --- |
| Daily statistics | [Arcanum](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/statistics/daily_stats)
| Text statistics | [Arcanum](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/statistics/text_stats)

### Logbroker
| log | staging | topic |
| --- | --- | --- |
| Events log | stable | [/maps_core_jams_infopoints/stable/infopoint-events-tskv](https://logbroker.yandex-team.ru/logbroker/accounts/maps_core_jams_infopoints/stable/infopoint-events-tskv) |
| Events log | testing | [/maps_core_jams_infopoints/testing/infopoint-events-tskv](https://logbroker.yandex-team.ru/logbroker/accounts/maps_core_jams_infopoints/testing/infopoint-events-tskv)|
| Shown events log | stable | [/maps_core_jams_infopoints/stable/infopoint-shown-events-tskv](https://lb.yandex-team.ru/logbroker/accounts/maps_core_jams_infopoints/stable/infopoint-shown-events-tskv) |
| Shown events log | testing | [/maps_core_jams_infopoints/testing/infopoint-shown-events-tskv](https://lb.yandex-team.ru/logbroker/accounts/maps_core_jams_infopoints/testing/infopoint-shown-events-tskv)|
| Iss log | stable | [/maps_core_jams_infopoints/stable/infopoint-iss-tskv](https://logbroker.yandex-team.ru/logbroker/accounts/maps_core_jams_infopoints/stable/infopoint-iss-tskv)|
| Iss log | testing | [/maps_core_jams_infopoints/testing/infopoint-iss-tskv](https://logbroker.yandex-team.ru/logbroker/accounts/maps_core_jams_infopoints/testing/infopoint-iss-tskv)|

### Настройки PushClient на инстансе:
- [Активация кастомных конфигов PushClient](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/docker/install/etc/template_generator/config.d/50-infopoint-setup.yaml)
- [Конфиг PushClient Events log](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/docker/install/etc/template_generator/templates/etc/yandex/statbox-push-client/custom/push-client-infopoint-events.yaml)
- [Конфиг PushClient Shown events log](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/docker/install/etc/template_generator/templates/etc/yandex/statbox-push-client/custom/push-client-infopoint-shown-events.yaml)

### Logfeller

#### Аккаунты
- [maps-core-jams-infopoints-events-log](https://yt.yandex-team.ru/hahn/accounts/general?account=maps-core-jams-infopoints-events-log)
- [maps-core-jams-infopoints-events-log-testing](https://yt.yandex-team.ru/hahn/accounts/general?account=maps-core-jams-infopoints-events-log-testing)

#### Вычислительный пул
- [logfeller-maps-infopoints](https://yt.yandex-team.ru/hahn/scheduling/overview?pool=logfeller-maps-infopoints&tree=physical)

#### Настройки поставки данных
- [Настройка стрима из Logbroker с указанием парсера](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/maps_infopoints_hahn_streams.json)
- [Настройка куда сохранять данные и с какой периодичностью](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/maps_infopoints_hahn_logs.json)
- [Настройка какие ресурсы использовать в stable](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/maps_infopoints_stable_project.json)
- [Настройка какие ресурсы использовать в testing](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/maps_infopoints_testing_project.json)
- [Конфиг полей кастомного парсера](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/maps_core_jams_infopoint-events-tskv-log.json)
- [Конфиг парсера ](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/parsers.auto.json) (см. `maps_core_jams_infopoint-events-tskv-log`)


## Secrets
Все секреты хранятся в [секретнице](https://yav.yandex-team.ru/) и доставляются в процесс infopoint средствами няни через переменные окружения. Сейчас секреты в няне управляются вручную описанием секретов в web ui в секции `Instance Spec -> Environment variables configuration`, при желании можно передать [управление секретами Sedem'у](https://wiki.yandex-team.ru/geo-infra/sedem/faq/#sekrety) (важно: sedem затирает секреты в няне, заданные вручную, поэтому переносить под управление sedem'ом нужно все секреты сразу).
| Staging | db | tvm | YT token |
| --- | --- | --- | --- |
| stable | [maps-core-jams-infopoints-db-stable](https://yav.yandex-team.ru/secret/sec-01e3mq2dgf7e5frzgj4wdeg9xv/explore/versions) | [maps-jams-infopoint-production-tvm](https://yav.yandex-team.ru/secret/sec-01deq29yspj3kez8ga4jayqn86) | [maps-jams-infopoint-stable-yt-token_from_maps_info](https://yav.yandex-team.ru/secret/sec-01e0zddms9vvahh8mahw4nn5sh/explore/versions) |
| testing | [maps-core-jams-infopoints-db-testing](https://yav.yandex-team.ru/secret/sec-01e3jqm76s09nasp7fthg52t92/explore/versions) | [maps-jams-infopoint-testing-tvm](https://yav.yandex-team.ru/secret/sec-01decbrgr9gz160s4tdy95ty8b/explore/versions) | [maps-jams-infopoint-testing-yt-token-from_maps_test_info](https://yav.yandex-team.ru/secret/sec-01e0zd38dvwn829npf8wrraz4q) |
| load | [maps-core-jams-infopoints-db-load](https://yav.yandex-team.ru/secret/sec-01e3n0aff7t8fq2yzy6mj5jdhz/explore/versions) | [maps-jams-infopoint-load-tvm](https://yav.yandex-team.ru/secret/sec-01e1yfnj9c36drygqred0nq57g/explore/versions) | не нужен (используется для отправки логов в YT) |
| unstable | [maps-core-jams-infopoints-db-unstable](https://yav.yandex-team.ru/secret/sec-01fa0e3rey0kd0f4ckaw9ptz4z/explore/versions) | [maps-jams-infopoint-unstable-tvm](https://yav.yandex-team.ru/secret/sec-01fa0pbsw8776jk9y6c13d44w3/explore/versions) | не нужен (используется для отправки логов в YT) |


## How to fix common problems
* Убедиться, что на основном разделе есть свободное место.
* Убедиться, что ecstatic датасеты активированы `/var/lib/yandex/maps/ecstatic/data`
* Если при switch-e возник hook failed, то повторяем деплой датасета с помощью [Sandbox задачи](https://sandbox.yandex-team.ru/task/566396281/view)
* Убедиться, что yacare сервис infopoint запущен, при необходимости перезапустить:
    * `sudo yacare restart infopoint`
* Проверить лог tie-events на наличие ошибок, убедиться, что ecstatic датасет `yandex-maps-jams-events` раскатился, ошибки дублирования датасета допустимы, смотри документацию к tie-events в этом документе.
* Иногда события добавляются нормально, но не успевают попасть на карту или попадают в измененном виде из-за модерации. Для проверки факта модерации стоит посмотреть лог infopoint'а на наличие `POST /v2/apply_moderation_verdicts`.<br>
* Если legacy import завершается с ошибкой `HTTP 500 SOME_EXTERNAL_SERVICE unreachable`, возможно `SOME_EXTERNAL_SERVICE` доступен только по ipv4, в RTC необходимо проверить, что включен DNS64: в няне в `Instance Spec` -> `Source type for resolv.conf` должен быть выбран `NAT64`
### Возможные проблемы с MongoDB
* Проблемы с бд можно диагностировать по сообщениям в логах infopoint'а: либо сервис не запускается вовсе и в логе упомянута проблема подлкючения к реплике mongodb, либо сервис запущен, но в логах появляются ошибки вроде `HTTP 500 Database error`
* При проблемах с кластером MongoDB стоит писать [команде MDB](https://wiki.yandex-team.ru/mdb/)
* Восстановить базу из регулярной резервной копии можно по инструкции [отсюда](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/database/readme.md)


## How to test
### TestApp
Для загрузки TestApp необходим основной yandex аккаунт привязанный к рабочему, тестировать на экранах RoadEvents и Driving.<br>
| Staging | URL (действительны и для iOS) |
|---|---|
| stable | [master](https://beta.m.ya.ru/ymta/master) |
| datatesting | [master\_datatesting](https://beta.m.ya.ru/ymta/master_datatesting) |
| testing | [master\_testing](https://beta.m.ya.ru/ymta/master_testing) |
### HTTP
**Получить список всех точек в формате XML**<br>
`curl -H "Host: infopoints.maps.yandex.net" <INFOPOINTS_HOST>/1.x/points/ > points.xml`

**Получить список всех точек в формате protobuf**<br>
`curl -H "Host: infopoints.maps.yandex.net" <INFOPOINTS_HOST>/events/list > points.pb`<br>
Декодировать полученный список:<br>
`cat points.pb | ~/arc/arcadia/contrib/tools/protoc/protoc -I ~/arc/arcadia/maps/doc/proto --decode=yandex.maps.proto.common2.response.Response ~/arc/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto`

**Добавить дорожное событие**<br>
1. Получить `Service-Ticket`
    ```sh
    ya tool tvmknife get_service_ticket sshkey -s <infopoint_tvm_id> -d <infopoint_tvm_id>

    # Информация:
    # <infopoint_tvm_id>:
    #   Load:       2018796
    #   Stable:     2012214
    #   Testing:    2012230
    #   Unstable:   2029142
    ```

2. Получить [OAuth token](https://oauth.yandex.ru/authorize?response_type=token&client_id=197a1215fa504edc982da3a464800ab1)

3. Получить `User-Ticket`
    ```sh
    echo '<token>' | ya tool tvmknife get_user_ticket oauth -b <blackbox> --tvm_id=<infopoint_tvm_id>

    # Информация:
    # <blackbox>:
    #   Test:       'blackbox-mimino.yandex.net'
    #   Prod:       'blackbox.yandex.net'
    #   Stress:     'blackbox-stress.yandex.net'
    #   Unstable:   'blackbox-test.yandex.net'
    ```

4. Перейти по соответствующей ручке
    ```sh
    curl -H "Host: infopoints.maps.yandex.net" -X POST -H "X-Ya-User-Ticket: <user_ticket>" -H 'X-Ya-Service-Ticket: <service-ticket>' '<INFOPOINTS_HOST>/events/add?ll=50,50&ull=50,50&type=chat&description=some_text&lang=ru_RU'
    ```


## How to add new supplier
* Добавить партнера в [конфиг агрегатора инфоточек](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/conf/suppliers.conf).
  * Urn::uuid генериттся случайным образом на предыдущем пункте тулзой uuidgen.
  * href должен начинаться с `http://` или `https://`. Иначе перходить будет на `https://yandex.ru/maps/<href>`
* После коммита `suppliers.conf` автоматически соберётся новая версия докера.
* Спросить у [Игоря Ретинского](https://staff.yandex-team.ru/retinskii), можно ли катить в stable.
* Выкатить новую версию в тестинг используя SEDEM. И подождать 24 часа.
* Выкатить версию в stable использую SEDEM.


## Documentation
[Старая документация, общая](https://wiki.yandex-team.ru/JandeksKarty/Projects/probki/points/)<br>
[Старая документация, REST API](https://wiki.yandex-team.ru/JandeksKarty/Projects/probki/points/pointsaggregation/externalinterface/)<br>
[Старая документация, агрегация](https://wiki.yandex-team.ru/JandeksKarty/Projects/probki/points/pointsaggregation/)<br>
[Старая документация 4](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/mapsinfopoint/)<br>
В сервисе используется 2 версии протокола: 1.x (сериализация событий в xml) и 2.x (сериализация событий в protobuf), но модерация событий и импорт списка событий доступны только по 1.x (добавление событий по одному доступно по 2.x). Данные хранятся в mongodb в Yandex.Cloud, никакого внутреннего кэша не используется, пользователи могут видеть только то, что лежит в mongodb.<br>
Авторизация пользователей выполняется через blackbox.<br>
Каждое дорожное событие имеет уникальный id. При определенных обстоятельствах дорожные события могут склеиваться (например, если 2 пользователя ставят событие "камера" на небольшом расстоянии друг от друга). При добавлении события с id=X возможны 2 сценария:<br>
    1) событие не склеивается с другим событием, тогда в базу записывается событие c id=X (назовем его "агрегированное"), у этого события есть поле points, которое содержит копию добавляемого события и тоже имеет id=X (назовем это событие "вложенное")<br>
    2) событие склеивается с другим событием id=Y, тогда агрегированное событие с id=Y обновляется, в список его вложенных событий добавляется событие с id=X, id агрегированного события может остаться Y, а может измениться на X в зависимости от того, какое событие считается более достоверным.<br>
    Некоторые ручки дергаются регулярно по крону (docker/install/etc/template_generator/templates/etc/supervisor/conf.d/infopoints_cron_imports.conf).<br>
    Каждая точка имеет время начала и окончания действия (в коде begin/end).
### Основные ручки
#### 1.x
| Path | Description |
|---|---|
| `GET /1.x/points/` | получить список всех агрегированных событий (XML)
| `POST /1.x/points/` | добавить дорожное событие, событие описывается в теле запроса (XML) |
| `PUT /1.x/points/uX/` | измененить (модерировать) агрегированное событие у которого есть вложенное событие с id=X, новое событие описывается в теле запроса (XML) |
| `GET /1.x/points/uX/` | получить агрегированное событие у которого есть вложенное событие с id=X (XML) |
| `DELETE /1.x/points/uX/` | удалить агрегированное событие у которого есть вложенное событие с id=X |
| `GET /1.x/legacy/?partner_uri=X` | импортировать список событий от поставщика c uri=X (XML) |
| `GET /1.x/cleaner/` | удалить агрегированные события у которых момент окончания действия раньше текущего момента (устаревшие события) |
| `PUT /1.x/users/X/ban/` | повесить на пользователя с uri=X бан (невозможность добавлять, удалять или изменять контент), бессрочный или временный, в зависимости от параметров запроса |
| `DELETE /1.x/users/X/ban/` | снять с пользователя с uri=X бан |
| `POST /1.x/points/uX/comments/` | добавить комментарий в теле запроса к точке с id=X (XML) |
| `DELETE /1.x/points/uX/comments/Y/` | удалить комментарий с id=Y у точки с id=X |
#### 2.x
| Path | Description |
|---|---|
| `GET /events/get` | получить 1 агрегированное событие или список агрегированных событий (в зависимости от наличия поля id), если есть аргумент id, то ищется агрегированное событие у которого есть вложенное событие с таким id (protobuf) |
| `GET /events/list` | то же, что и GET /events/get |
| `POST /events/add` | добавить дорожное событие, событие описывается в параметрах запроса |
| `POST /comments/add` | добавить комментарий к точке (параметры передаются в параметрах запроса) |
| `GET /comments/list?event_id=X` | получить комментарии к точке с id=X |
| `POST /events/vote?event_id=X` | проголосовать за точку с id=X |
| `GET /wipe_data` | удалить все данные из коллекций `users` и `points` (в коде запрещено вызывать в stable), требует наличия флага `allow_wipe_data` в settings.conf, иначе forbidden. Ручка должна использоваться исключительно для стрельб. |
#### v2
| Path | Description |
|---|---|
| `POST /v2/apply_moderation_verdicts` | применить список вердиктов модерации |
### GDPR
| Path | Description |
|---|---|
| `GET /1/takeout/status/` | Отдает статус данных пользователя `[empty, ready_to_delete, delete_in_progress]` |
| `POST /1/takeout/delete/` | Запрос на удаление данных пользователя |
| `POST /1/takeout/export/` | Выдает все имеющиеся данные для конкретного пользователя |

### Legacy import
Legacy import - Основной механизм импорта большого (>1) числа событий, в том числе импорт из НЯКа и от партнеров вроде gati.<br>
Почему legacy импорт называется legacy - потому что, но другого метода импорта нескольких точек за раз нет (кроме добавления по одной через соответсвтующие ручки).<br>
Cписок партнеров указан в [maps/infopoint/conf/partners.conf](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/conf) и они же должны находится в [maps/infopoint/conf/suppliers.conf](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/conf/suppliers.conf) с типом пользователя PARTNER, EXPERT или MODERATOR.<br>
События при legacy импорте не склеиваются никогда, в отличие от событий, которые ставят пользователи. Склеивание событий от партнеров ведет к большому числу потенциальных проблем и чаще всего не имеет смысла [MAPSCORE-4750](https://st.yandex-team.ru/MAPSCORE-4750).<br>
Основная масса событий (в первую очередь камер) импортируются из НЯКа; xml файл, указанный в partners.conf для НЯКа, создается огородным модулем [export_cams](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/export_cams). Помимо камер также импортируются школы [export_schools](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/export_schools).<br>
В качесте хранилища эти модули используют S3

### Импорт расписания разведения мостов
Есть несколько мостов с разными интервалами разведения, необходимо для каждого моста, пока они еще сведены, отображать серую иконку (в описании к иконке писать временной интервал, когда мост будет разведен), а в интервал, когда мост разведен, - отображать цветную иконку и отдавать событие с типом drawbridge в списке запрошенных событий (необходимо для маршрутизатора). Сейчас это делается так: непосредственно после сведения каждого моста создается новое дорожное событие (дергается соответствующая ручка) с типом drawbridge со временем начала действия (begin) - момент следующего разведения, и временем окончания (end) - момент сведения, тогда до разведения мостов событие будет "событие в будущем" и его можно отображать серым цветом, во время интервала разведения событие будет "текущим" и его можно отображать цветным и рассчитывать маршрут с учетом разведенных мостов; сразу после сведения добавляется следующее событие разведения и так по кругу. Добавлять событие drawbridge для нескольких мостов одновременно через legacy import пока не представляется возможным, потому что для каждого моста следующее событие должно добавляться сразу после окончания предыдущего, а так как время сведения у мостов разное, то добавление выполняется по одному. Управлением дорожными событиями drawbridge занимается сервис АРМ.
### Локализация
Переводы хранятся [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/i18n)<br>
Заказываются [в танкере](https://tanker.yandex-team.ru/?project=maps&branch=master&keyset=infopoints)<br>
Локаль перевода задается в параметре `lang` запроса, например, `infopoints.maps.yandex.net/events/get?event_id=XXX&lang=tr_TR` (`ru_RU` по умолчанию)
### Выгрузка UGC по GDPR (старый вариант сервиса, будет разобран).
[Регулярная выгрузка UGC в YT](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/tools/ugc_extractor)<br>
[Сервис для выдачи данных из YT по uid](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/takeout)
### GDPR
Паспорт предоставляет возможность пользователям выгружать произведенный ими контент, а также удалять его.

Для ручек `/1/takeout/status/` и `/1/takeout/delete/` идентификация производится по Service-Ticket и User-Ticket.

Для ручки `/1/takeout/export/` идентификация производится по Service-Ticket и url параметру uid

Документация Паспорта про GDPR
[Схема подключения takeout](https://wiki.yandex-team.ru/passport/takeout/integration/#sinxronnyjjmexanizmvygruzkidannyx)
[Схема подключения delete](https://wiki.yandex-team.ru/users/yakushevsky/takeoutrequirements/)

### Как проверить status/delete на бэкендах
1. Получить `Service-Ticket`
    ```sh
    ya tool tvmknife get_service_ticket sshkey -s <infopoint_tvm_id> -d <infopoint_tvm_id>

    # Информация:
    # Требуется роль tvm ssh пользователь в abc infopoint
    # <infopoint_tvm_id>: tvm id инфопоинта для нужного staging-а (взять из tvmtool.conf)
    ```

    `В testing окружении можно не передавать service-ticket в заголовках для удобства разработки.`

2. Получить [OAuth token](https://oauth.yandex.ru/authorize?response_type=token&client_id=197a1215fa504edc982da3a464800ab1)

3. Получить `User-Ticket`
    ```sh
    echo '<token>' | ya tool tvmknife get_user_ticket oauth -b <blackbox> --tvm_id=<infopoint_tvm_id>

    # Информация:
    # Требуется роль tvm ssh пользователь в abc infopoint
    # <blackbox>: 'blackbox-mimino.yandex.net'/'blackbox.yandex.net'
    # <infopoint_tvm_id>: tvm id инфопоинта для нужного staging-а (взять из tvmtool.conf)
   ```
4. Зайти на машинку в нужном окружении
5. Перейти по соответствующей ручке
    ```sh
    curl --output - -H "Host: infopoints.maps.yandex.net" -H "X-Ya-User-Ticket: <user_ticket>" -H 'X-Ya-Service-Ticket: <service-ticket>' 'localhost/1/takeout/status/'

    curl --output - -H "Host: infopoints.maps.yandex.net" -H "X-Ya-User-Ticket: <user_ticket>" -H 'X-Ya-Service-Ticket: <service-ticket>' 'localhost/1/takeout/delete/'
    ```

### Как проверить export/status/delete через passport

Перейти на стенд паспорта, используя логин вручную созданного пользователя в production Паспорте.
Пользователи, созданные через TUS, работать не будут. Также не будут работать пользователи созданные в testing Паспорте.
- [testing](https://passport-test.yandex.ru/profile/data)
- [prod-rc](https://passport-rc.yandex.ru/profile/data)
- [prod](https://passport.yandex.ru/profile/data)

В разделе `Удаление данных` выбрать `Карты` (может быть под катом `Остальные сервисы`). В Картах найти `Дорожные события`.
Если данных нет, будет отображена информация `Данных нет`. В таком случае, можно поставить дорожное событие, например, через TestApp.
После этого данные можно будет удалить.

Для выгрузки данных нажать `Скачать данные`. В среднем занимает 1 сутки, бывает меньше.


### Как проверить выгрузку на бэкендах
1. Получить `Service-Ticket`
    ```sh
    ya tool tvmknife get_service_ticket sshkey -s <infopoint_tvm_id> -d <infopoint_tvm_id>

    # Информация:
    # Требуется роль tvm ssh пользователь в abc infopoint
    # <infopoint_tvm_id>: tvm id инфопоинта для нужного staging-а (взять из tvmtool.conf)
    ```

    `В testing окружении можно не передавать service-ticket в заголовках для удобства разработки.`
2. Зайти на машинку в нужном окружении
3. Сходить на ручку export
    ```sh
    curl --output - -X POST -H "Host: infopoints.maps.yandex.net" -H 'X-Ya-Service-Ticket: <service-ticket>' 'localhost/1/takeout/export/?uid=<uid>'
    ```

### Как проверить выгрузку через passport
1. Получить `Service-Ticket`
    ```sh
    # testing
    ya tool tvmknife get_service_ticket sshkey -s 2012230 -d 2009783
    # production
    ya tool tvmknife get_service_ticket sshkey -s 2012214 -d 2009785
    
    # Информация:
    # Требуется роль tvm ssh пользователь в abc infopoint
    ```
2. Сходить с ним в паспорт
    ```sh
    # testing
    curl -X POST 'https://takeout-test.passport.yandex.net/1/debug/run_integration_test/?consumer=maps-core-jams-infopoints' -d 'uid=<uid>&service_name=maps-core-jams-infopoints' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
    # production
    curl -X POST 'https://takeout.passport.yandex.net/1/debug/run_integration_test/?consumer=maps-core-jams-infopoints' -d 'uid=<uid>&service_name=maps-core-jams-infopoints' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
    ```
3. Запросить результат теста, передав extract_id полученный на предыдущем шаге
    Тест не отдает результаты выгрузки, а только проверяет, получилось ли ее сделать
    ```sh
    # testing
    curl -X POST 'https://takeout-test.passport.yandex.net/1/debug/get_status/?consumer=maps-core-jams-infopoints' -d 'uid=<uid>&service_name=maps-core-jams-infopoints&extract_id=<extract_id>' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
    # production
    curl -X POST 'https://takeout.passport.yandex.net/1/debug/get_status/?consumer=maps-core-jams-infopoints' -d 'uid=<uid>&service_name=maps-core-jams-infopoints&extract_id=<extract_id>' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
    ```
[Документация](https://wiki.yandex-team.ru/passport/takeout/integration/#testirovanieintegracii) по интеграционному тестированию через паспорт

### tie-events
[Исходники](https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/tools/tie-events)<br>
Маршрутизатор и рендерер потребляют данные из infopoint'а не напрямую, а через ecstatic датасет `yandex-maps-jams-events`, который генерируется бинарником tie-events. Скрипт генерации датасета запускается по [крону](https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/tools/tie-events/bin/cron/cron.d) раз в несколько минут на каждой из кондукторской машин (что приводит к ошибке раскатки датасета на 2х из 3х машин из-за дублирования версии датасета, это ожидаемое поведение).<br>
tie-events выгружает из infopoints все события (возможно, предварительно фильтруя их, например, по confidence события), привязывает их к дорожному графу и раскатывает датасет.
### Модерация
Модерация событий и комментариев выполняется частично в автоматическом, а частично в ручном режиме.
#### Автомодерация
Выполняется в основном коде сервиса в момент добавления событий/комментариев без участия cleanweb'а на основе тривиальных правил, например, не допускается добавление разговорчиков без описания или автоматически одобряется добавление событий с тэгом `{"accident"}` с пустым описанием или указанием только рядов в описании.
#### Модерация через чистый веб
[Документация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/moderation/readme.md)
### ratelimiter
[ratelimiter](https://abc.yandex-team.ru/services/maps-core-ratelimiter) устанавливает и контролирует лимит на rps сервиса (защита от перегруза), при превышении которого yacare начинает отвечать кодом 429.<br>
[Документация yacare по ratelimiter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/yacare#ratelimiter) и по самому [ratelimiter](https://wiki.yandex-team.ru/geo-infra/ratelimiter2-manual/).<br>
Конфинг ratelimiter'а для infopoints лежит [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/infopoint), после мержа изменений в транк новые лимиты начинают действовать примерно через 10 минут (по завершению sandbox задач `MAPS_RATE_PANELS_REFRESHER` и `MAPS_RATE_LIMITS_REFRESHER`, автору комита придет письмо).<br>
Графики [здесь](#graphics).


## How to release new soft
### infopoint
* Переходим в папку infopoints `cd ~/arc/arcadia/maps/infopoint`
* Комитим изменения в trunk (про хотфикс - смотри чуть ниже)
* Ждем завершения sandbox задачи `MAPS_DOCKER` (ее запустит TestEnv, по завершению должно прийти письмо на почту)
* Смотрим зарелизенную версию `ya tool sedem release info .`
* Делаем `ya tool sedem release start .` (создаст новый бранч с trunk-а, тикет в StarTrek, дифф в wiki и т.п. )
* Ждем пока появится `V <version>.x` в `ya tool sedem release info .` (пример v1.1)
* Катим в тестинг `ya tool sedem release step . <version>.x testing` (пример: `ya tool sedem release step . 1.1 testing`)
* Катим в prestable `ya tool sedem release step . <version>.x prestable`
* Катим в stable `ya tool sedem release step . <version>.x stable`
* Если требуется сделать hotfix в уже существующую stable ветку:
  * Делаем по [инструкции](https://docs.yandex-team.ru/sedem/releases#hotfiksy-v-sedem-machine)
  * Если есть желание сброситься на предыдущую стабильную ветку, то `ya tool sedem release step --force . <prevVersion>.x stable`
* Всю информацию по работе с релизами в Sedem Machine [тут](https://docs.yandex-team.ru/sedem/releases)
### Как выкатить в unstable без комита в trunk
* Переходим в папку infopoints `cd ~/arc/arcadia/maps/infopoint/docker`
* Собираем образ и пушим в репозиторий `ya package pkg.json --docker --docker-push --docker-repository=maps` (в случае успеха в выводе команды будет указан тэг нового образа)
* В [Instance Spec](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_unstable/instance_spec) указываем тэг образа, собранного на предыдущем этапе
* Сохраняем новый Instance Spec и активируем новый snapshot

Наблюдать за ходом выкладки можно на дашборде из секции [instances](#instances).
### tie-events
- Выкатывается вместе с основным образом infopoints
### How to release fast
Иногда TestEnv обнаруживает изменения в директории проекта с большой задержкой (вплоть до нескольких часов). Если нужно гарантировано выкатить фикс в короткие сроки, то:
* Комитим изменения в транк
* Клонируем sandbox задачу `MAPS_DOCKER`, например, [эту](https://sandbox.yandex-team.ru/task/660747460/view)
* Меняем во всех полях заготовки задачи номер SVN ревизии на номер из нашего комита (`merged as`) и жмакаем Run
* По завершению задачи следуем инструкции выше
### How to release bypassing trunk
Если нужно выкатить крайне срочно или в обход комита в транк (только если знаешь, что ты делаешь):<br>
```
cd ~/arc/arcadia/maps/infopoint/docker && \
ya package pkg.json --docker --docker-push --docker-repository=maps
```
В логе сборки будет указан тэг собранного образа в репозитории maps, этот тэг прописываем в Instance Spec в няне

## Known clients
* [Mobile proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/)
* Маршрутизатор и Рендерер пробок (слой дорожных событий) потребляют ecstatic датасет yandex-maps-jams-events
* Клиентские браузеры (БЯК) обращаются к рендереру пробок (слой дорожных событий)
    * [production](https://maps.yandex.ru)
    * [testing](https://l7test.yandex.ru/maps)
* [Автоматическое Рабочее Место](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/arm20/) АРМ, ARM
* [Генератор гипотез](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/infopoints_hypgen) - генерация гипотез о дорожных перекрытиях на основе дорожных событий и фидбека


## SLA
[SLA script](https://a.yandex-team.ru/arc_vcs/maps/infra/monitoring/sla_calculator/core/services/maps_core_jams_infopoints.py)<br>
[Report in stat](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_jams_infopoints?scale=d&_incl_fields=d1&_incl_fields=d30&_incl_fields=d7&_incl_fields=n1&_incl_fields=n30&_incl_fields=n7&_period_distance=30)


## Ecstatic Datasets
* yandex-maps-geodata6 - используется infopont'ом для определения timezone'ы по id региона и региона клиента по ip
* yandex-maps-coverage5-geoid - используется infopoint'ом и tie-events'ом для работы с регионами, например:
    * найти id региона по точке на карте
    * отфильтровать комментарии по региону
* yandex-maps-coverage5-trf - потребляются tie-events'ом
* yandex-maps-geobase-tzdata - потребляются infopoint-ом для форматирования времени.
* yandex-maps-jams-events - генерируется tie-events'ом (дорожные события, привязанные к дорожному графу)
* Дорожный граф (потребляется tie-events'ом):
    * yandex-maps-graph-activator
    * yandex-maps-graph-compact
    * yandex-maps-graph-compact-edges-persistent-index
    * yandex-maps-graph-compact-rtree


## Балансеры
### L3
| Staging | URL |
|---|---|
| stable | [infopoints.maps.yandex.net](https://l3.tt.yandex-team.ru/service/2495) |
| testing | [infopoints.tst.maps.yandex.ru](https://l3.tt.yandex-team.ru/service/305) |
### L7
| Staging | AWACS | YASM |
|---|---|---|
| stable | [core-jams-infopoints.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-infopoints.maps.yandex.net/show/) | [core-jams-infopoints.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-infopoints.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas;prj=maps-core-jams-infopoints;signal=service_total) |
| testing | [core-jams-infopoints.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-infopoints.testing.maps.yandex.net/show/) | [core-jams-infopoints.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-infopoints.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas;prj=core-jams-infopoints-testing-maps;signal=service_total) |


## Firewall macroses
| Staging | URL |
|---|---|
| stable | [`_MAPS_CORE_JAMS_INFOPOINTS_STABLE_RTC_NETS_`](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_INFOPOINTS_STABLE_RTC_NETS_) |
| testing, load, unstable | [`_MAPS_CORE_JAMS_INFOPOINTS_TESTING_RTC_NETS_`](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_INFOPOINTS_TESTING_RTC_NETS_) |


## Regression Stress Testing
Больше доки [тут](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/regression/readme.md).<br>
| Type | URL |
|---|---|
| Graphics | [lunapark](https://lunapark.yandex-team.ru/regress/MAPSNAVI?service=maps-jams-infopoints) |
| Autoshootings | [sandbox](https://sandbox.yandex-team.ru/scheduler/20332/view) |
| Ammo generation script | [script](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/regression/requestgen) |

Если хочется внести изменения в Sandbox задачу без коммита в транк, достаточно:
* поправить локально [код sandbox задачи](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsInfopointShooting/__init__.py)
* сделать локально ya make
* проверить наличие нужного тега `./MapsInfopointShooting content --list-types | grep MAPS_INFOPOINT_SHOOTING`
* загрузить бинарник в sandbox `./MapsInfopointShooting upload`
* склонировать [sandbox задачу](https://sandbox.yandex-team.ru/task/624728159/view) и в настройках Advanced выставить id загруженного ресурса `Tasks archive resource`
* запустить задачу

Приведенный выше гайд не сработает, если изменится, например, набор параметров sandbox задачи. В таком случае нужно делать коммит в trunk

### S3
Для [abc infopoint](https://abc.yandex-team.ru/services/maps-core-jams-infopoints/) выделена [квота в  S3](https://dispenser.yandex-team.ru/db/projects/maps-core-jams-infopoints), в который огородные модули export_cams и export_schools выгружают данные.<br>
Как работать с S3 можно посмотреть в [доке](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/).<br>
Работать с бакетами можно только с помощью ключей.<br>
Ключи для S3 лежат [здесь](https://yav.yandex-team.ru/secret/sec-01f290rt39ghe3r3ksyq8dvnsy/)<br>
Эти ключи имеют роль `admin`. Подробнее про все роли можно посмотреть [здесь](https://wiki.yandex-team.ru/mds/s3-api/authorization/#vydachapravrobotuilisotrudniku)

### Полезные ссылки про sandbox
- [Официальый док](https://wiki.yandex-team.ru/sandbox/tasks/binary/)
- [Про бинарную сборку тасок](https://clubs.at.yandex-team.ru/arcadia/16437)
- [Где следить](https://beta-testenv.yandex-team.ru/project/sandbox-trunk/job/BUILD_SANDBOX_TASKS/history?limit=20) когда соберется наш тип задачи после коммита в trunk
- [Где сделать clear cache](https://sandbox.yandex-team.ru/preferences), если задача собралась, но не появилась в sandbox

### Квота sandbox
[MAPS-CORE-ROAD-EVENTS](https://sandbox.yandex-team.ru/admin/groups/MAPS-CORE-ROAD-EVENTS/general)

### Антиробот
Снижает нагрузку на поисковые мощности за счет выявления и ограничения деятельности автоматов. Использует Matrixnet формулу определения роботности запроса. Полное описание сервиса можно посмотреть [здесь](https://wiki.yandex-team.ru/jandekspoisk/sepe/antirobotonline/).<br>
При блокировке запроса Антироботом, вернется 403 ошибка, их можно посмотреть на [графике L7](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-infopoints.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla;prj=maps-core-jams-infopoints;signal=service_total).<br>
[График Антиробота](https://yasm.yandex-team.ru/template/panel/antirobot_for_service/service=maps_core)

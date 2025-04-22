# Сбор логов о событиях загрузки, изменения и просмотра ugc-контента в MRC

Здесь описана реализация в MRC требований к "Организаторам Распорстранения Информации" ([тикет](https://st.yandex-team.ru/MAPSMRC-3286), [официальные требования](https://h.yandex-team.ru/?http%3A%2F%2F97-fz.rkn.gov.ru%2Forganizer-dissemination), [описание на wiki](https://wiki.yandex-team.ru/shumi/datalog97fz/)).

Результирующий лог собирается в YT-таблицах внутри директории [//home/logfeller/logs/maps_core_nmaps_mrc_stable_ugc_events_json](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps_core_nmaps_mrc_stable_ugc_events_json).

## Что логируем

Логируются события создания, обновления, удаления и просмотра фотографий пользователей. Для событий сохраняются следующие поля:
- `timestamp` - время события (unix time)
- `user_ip` - IP-адрес пользователя
- `user_port` - порт пользователя
- `user_uid` - UID пользователя
- `action` - действие пользователя, возможные события: `create`, `view`, `update`, `delete`.
- `object_type` - тип объекта, пока используется только `photo`
- `object_id` - идентификатор объекта.

## Процесс доставки данных в YT

Сбор логов в YT-таблицы реализован по схеме: `Service -> log_file -> push-client -> LogBroker -> Logfeller -> YT` ([документация по подключению](https://wiki.yandex-team.ru/logfeller/connection/)).

Логирование операций пользователя распределено по нескольким сервисам:
- [agent-proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/agent-proxy) -- логирует события загрузки новых объектов из мобильных приложений.
- [browser](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/bin) -- логирует события просмотра объектов через НЯК, БЯК, МЯК.
- [ugc_back](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/ugc_back) -- логирует события просмотра объектов через ЛК в БЯК.
- [long_tasks](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks) -- логирует удаления и обновления объектов асинхронными операциями, запущенными из `ugc_back`.

| Staging | Logbroker topic | Logfeller monitoring | YT |
| ------- | --------------- | -------------------- | -- |
| testing | [maps_core_nmaps_mrc/testing/ugc_events_json](https://logbroker.yandex-team.ru/logbroker/accounts/maps_core_nmaps_mrc/testing/ugc_events_json?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1618744625010&metricsTo=1618831025010&sortOrder=%22default%22) | [maps_core_nmaps_mrc@testing-ugc_events_json](https://monitoring.yandex-team.ru/projects/logfeller/dashboards/mon3ge2tr6pmb7fit8b3?p.cluster=hahn&p.service=%2A&p.stream-name=maps_core_nmaps_mrc%40testing-ugc_events_json&range=1d&refresh=60) | [//home/logfeller/logs/maps_core_nmaps_mrc_testing_ugc_events_json](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps_core_nmaps_mrc_testing_ugc_events_json) |
| stable | [maps_core_nmaps_mrc/stable/ugc_events_json](https://logbroker.yandex-team.ru/logbroker/accounts/maps_core_nmaps_mrc/stable/ugc_events_json?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1618744760901&metricsTo=1618831160901&refreshInterval=60&sortOrder=%22default%22) | [maps_core_nmaps_mrc@stable-ugc_events_json](https://monitoring.yandex-team.ru/projects/logfeller/dashboards/mon3ge2tr6pmb7fit8b3?p.cluster=hahn&p.service=%2A&p.stream-name=maps_core_nmaps_mrc%40stable-ugc_events_json&range=1d&refresh=60) | [//home/logfeller/logs/maps_core_nmaps_mrc_stable_ugc_events_json](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps_core_nmaps_mrc_stable_ugc_events_json) |


### Настройки push-client на сервисах

| service | push-client configs |
| ------- | ------------------- |
| maps_core_nmaps_mrc_agent_proxy | [mrc-ugc-events-uploader.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/agent-proxy/docker/install/etc/template_generator/templates/etc/yandex/statbox-push-client/custom/mrc-ugc-events-uploader.yaml)<br>[mrc-ugc-events-yacare.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/agent-proxy/docker/install/etc/template_generator/templates/etc/yandex/statbox-push-client/custom/mrc-ugc-events-yacare.yaml) |
| maps_core_nmaps_mrc_browser | [mrc-ugc-events.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/bin/docker/install/etc/template_generator/templates/etc/yandex/statbox-push-client/custom/mrc-ugc-events.yaml) |
| maps_core_nmaps_mrc_long_tasks | [mrc-ugc-events.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/docker/install/etc/template_generator/templates/etc/yandex/statbox-push-client/custom/mrc-ugc-events.yaml) |
| maps_core_nmaps_mrc_ugc_back | [mrc-ugc-events.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/ugc_back/docker/install/etc/template_generator/templates/etc/yandex/statbox-push-client/custom/mrc-ugc-events.yaml) |


### Настройки logfeller

- [конфиг парсера](https://a.yandex-team.ru/arc_vcs/logfeller/configs/parsers/maps_core_mrc_ugc-events-json-log.json)
- [конфиги стримов maps_core_nmaps_mrc/testing/ugc_events_json, maps_core_nmaps_mrc/stable/ugc_events_json](https://a.yandex-team.ru/arc_vcs/logfeller/configs/logs/common_hahn_streams.json)
- [конфиги логов maps_core_nmaps_mrc_testing_ugc_events_json, maps_core_nmaps_mrc_stable_ugc_events_json](https://a.yandex-team.ru/arc_vcs/logfeller/configs/logs/common_hahn_logs.json)

# Где находятся логи в yt?
* [production 30 min](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/market-mdm-app-log-prod/30min)
* [production 1 day](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/market-mdm-app-log-prod/1d)
* [testing 30 min](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/market-mdm-app-log-test/30min)
* [testing 1 day](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/market-mdm-app-log-test/1d)
# Основные поля
## Поля, генерируемые LogFeller
* source_uri - позволяет определить, с какого из наших инстансов пришло сообщение. Не пугаться unknown_path - это наследие push-clinet, раньше указывало из какого файла пришло сообщение
## Поля, генерируемые нашим приложением
* thread
* timestamp - пишется, как строка в таймзоне UTC, поэтому на 3 часа меньше, чем в лог файле на инстансе (там Московское время)
* log_level
* logger
* message
* market-request-id
* other_fields - сюда попадут все неопознанные поля из наших логов
* error_type
* error_message
* stack_trace
## Описание пайплайна доставки
MDM -> Unified Agent log4j2 appender ->  Unified Agent -> Logbroker -> LogFeller -> YT

### Unified Agent log4j2 appender
[Документация](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/java/log4j2/USAGE.md)

Для облегчения парсинга в LogFeller, пишем в JSON с помощью [JSON Template Layout](https://logging.apache.org/log4j/2.x/manual/json-template-layout.html).

Не пишем дефолтные мета поля, так как они есть в теле сообщения.

### Unified Agent
[Документация](https://logbroker.yandex-team.ru/docs/unified_agent/)

Получает сообщения из appender-а по grpc через TCP сокет и отправляет в Logbroker. Может накапливать сообщения в буфере на диске (/logs/unified-agent-storage).

### HOW TO
{% cut "Как добавить свой логгер для поставки в YT" %}

Просто добавить аппендер `<AppenderRef ref="MDM_UNIFIED_AGENT_TO_YT_LOGS"/>` к своему логгеру.

{% endcut %}

{% cut "Где найти конфиги Unified Agent?" %}

[unified_client_config](https://a.yandex-team.ru/arc_vcs/market/mbo/mbo-category/mbo-mdm/src/main/external/unified_client_configs)

{% endcut %}

### Графики
* [Grafana](http://grafana.yandex-team.ru/goto/NtYVLLznk)

### Полезные/часто используемые YQL для логов
* [Ошибки чтения из логброкера (Datacamp -> MDM)](https://yql.yandex-team.ru/Operations/YSciRBJKfXo7mAWwDAC7ANFV0sgyuxZkx72wzJamTVc=)
* [Проверка синхронизации OLD_MDM params <-> BMDM metadata](https://yql.yandex-team.ru/Operations/YS3mBZwJyQoF87D3s12LVoxZqDav9alsCv62tRrxOTQ=)
* [Ошибки сохранения при эскпорте MDM -> MBO](https://yql.yandex-team.ru/Operations/YY1MiQVK8JQzpaR26ppMTql66wcnoaSqRnWBS_nHAJA=)
* [Статистика по мультивотчам с графиками расчета золота ssku](https://yql.yandex-team.ru/Operations/YPE11PMBw55cXHoF7GM8TzHynehFaEBfpgKgu9ok-8Q=)

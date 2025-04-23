# Core Feedback Api

Сервис для синхронизации фидбека на карты.
Есть api, [документация](https://docs.yandex-team.ru/maps-feedback/service/api), [рядом](https://docs.yandex-team.ru/maps-feedback/service/examples) примеры запросов.

Помимо документации работают 4 регулярных процесса:
* [Синхронизация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/sprav) со Справочником (фидбек на организации).
* [Синхронизация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/support) с сансарой.
* [Импорт](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/samsara_importer) фидбэка из сансары.
* [Рассылка нотификаций](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/notifications)

[Документация про процессы, которые происходят с фидбэком.](https://docs.yandex-team.ru/maps-feedback/service/workflow)

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Анна Ждан (likynushka@yandex-team.ru) <br> Алексей Пономарев (ponomarev@yandex-team.ru) |
| Отвественные SRE | Анна Ждан (likynushka@yandex-team.ru) <br> Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/feedback/api](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api) |
| Сервис в ABC | [maps-core-feedback-api](https://abc.yandex-team.ru/services/maps-core-feedback-api/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_FEEDBACK_API |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_feedback_api_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_feedback_api_stable/) | [ core-feedback-api.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-feedback-api-stable-panel-main/) | [ maps_core_feedback_api_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_feedback_api_stable) |
| Testing | [maps_core_feedback_api_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_feedback_api_testing/) | [ core-feedback-api.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-feedback-api-testing-panel-main/) | [ maps_core_feedback_api_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_feedback_api_testing) |

## Графики MDB
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps_feedback_prod](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=6f727507-606f-46a9-9ade-96ede15509d2;dbname=maps_feedback_prod) |
| Testing | [maps_feedback_test](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=a9cf95d2-4398-4273-b943-8b455bf1c38f;dbname=maps_feedback_test) |
| Unstable | [maps_feedback_prod](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbrqh3u3mb9oo0l8em4;dbname=maps_feedback_prod) |

[Ratelimiter](https://yasm.yandex-team.ru/template/panel/maps_core_feedback_api-ratelimiter2-panel)

[Monitorings all (tag=a_prj_maps-core-feedback-api)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-feedback-api)

| Staging | User panels |
| ------- | ----------- |
| ????    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-feedback-api.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-feedback-api.maps.yandex.net/) | [core-feedback-api.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-feedback-api.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man,vla;prj=core-feedback-api-maps;signal=service_total) | [rtc_balancer_core-feedback-api_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-api_maps_yandex_net_man)<br>[rtc_balancer_core-feedback-api_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-api_maps_yandex_net_sas)<br>[rtc_balancer_core-feedback-api_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-api_maps_yandex_net_vla) |
| Testing | Default | [core-feedback-api.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-feedback-api.testing.maps.yandex.net/) | [core-feedback-api.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-feedback-api.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-feedback-api-testing-maps;signal=service_total) | [rtc_balancer_core-feedback-api_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-feedback-api_testing_maps_yandex_net_sas) |


## What happens when service is down

* Не отправляется фидбек на объекты на карте
* Не отображается фидбек в народной карте и админке
* Не работает синхронизация фидбека со смежными сервисами
* Не отправляются пуши и письма на публикацию пользовательских правок

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/feedback-api/* |
| Gdpr worker | /var/log/yandex/maps/feedback-gdpr-worker/* |
| Notifications sender | /var/log/yandex/maps/feedback-notifications-sender/* |
| Samsara importer | /var/log/yandex/maps/feedback-samsara-importer/* |
| Sprav updater | /var/log/yandex/maps/feedback-sprav-updater/* |
| Support updater | /var/log/yandex/maps/feedback-support-updater/* |
| Synchronization tool | /var/log/yandex/maps/feedback-synchronization-tool/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2020-10-05` WHERE vhost LIKE 'core-feedback-api.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Стандартные мониторинги yacare-приложения чинятся стандартно: посмотреть в логи (`/var/log/yandex/maps/feedback-api/`), разобараться, что не так.

#### Кастомные мониторинги:

| Monitoring | Что показывает | Где искать логи | Исходники | Как чинить |
| ---------- | -------------- | --------------- | --------- | ---------- |
| `feedback-support-updater` | Синхронизация с сансарой. | `/var/log/yandex/maps/feedback-support-updater/` | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/support | Известная проблема - `Message: ERR: Cannot get samsara tickets: {"rc":"ERROR","description":"No access to queue <<queue number>> for user robot-wikimap"`. </br>Ничего сделать не можем, нужно идти к chdm@ и просить переложить тикеты в нужную очередь. Обсуждали в https://st.yandex-team.ru/NMAPS-11640 |
|`feedback-sprav-updater`| Синхронизация со Справочником  | `/var/log/yandex/maps/feedback-sprav-updater/` | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/sprav | Каждую конкретную ошибку надо смотреть в логах. Если в логах видны ошибки на стороне Справочника, нужно идти к sobols@.
| `feedback-samsara-importer` | Импорт фидбэка из Сансары. | `/var/log/yandex/maps/feedback-samsara-importer/` | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/samsara_importer | Надо смотреть в логах, что не так. Скорее всего, пытаемся импортировать невалидный тикет. С невалидным тикетом нужно идти к chdm@: просить убрать невалидный и настраивать процесс на стороне саппортов так, чтобы невалидные тикеты не возникали
| `feedback-notifications-sender` | Рассылка нотификаций. | `/var/log/yandex/maps/feedback-notifications-sender/` | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/notifications|
|`feedback-gdpr-worker` | Обработка GDPR-запросов. | `/var/log/yandex/maps/feedback-gdpr-worker/` | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/gdpr | Посмотреть логи gdpr-запросов, понять, что идёт не так
|`feedback-tools-alive` | Проверка живости всех процессов супервизора. Должна реагировать, если процесс падает не сразу после начала работы в отличие от стандартного supervisor-fatal мониторинга | | | Посмотреть supervisor status all, найти упавшие процессы, поднять обратно
|`feedback-nmaps-need-info-queue` | Размер очереди тикетов в статусе `need_info` | `/var/log/yandex/maps/feedback-support-updater/` | Мониторинг: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/monitoring/lib/queue_monitoring.cpp?rev=r8477996#L142</br>Тул: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/support | Скорее всего, проблема в том, что на стороне саппортов одновременно много открытых тикетов в сансаре. Надо в этом убедиться и понять, ок ли это. Со стороны саппорта ответственный chdm@
|`feedback-sprav-queue` | Размер очереди тикетов, которые ждут синхронизации со Справочником |  `/var/log/yandex/maps/feedback-sprav-updater/` | Мониторинг: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/monitoring/lib/queue_monitoring.cpp?rev=r8477996#L134</br>Тул: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/sprav | Известная проблема: после рассылки пушей на статусы организаций (обычно по пятницам) получаем сразу много фидбека, из-за чего очередь забивается. В общем случае надо понять, виноваты пуши или что-то мешает разбирать заявки в справочнике. Проблема может быть в туле, который разгребает, а может быть на стороне справочника
|`feedback-notifications-queue` | Размер очереди нотификаций, которые нужно отправить |  `/var/log/yandex/maps/feedback-notifications-sender/` | Мониторинг: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/monitoring/lib/queue_monitoring.cpp?rev=r8477996#L138</br>Тул: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/notifications | Посмотреть в логи и табилчку `feedback_notifications`, разобраться, почему не отправляются нотификации.
| `feedback-gdpr-requests-queue` | Размер очереди GDPR-запросов | `/var/log/yandex/maps/feedback-gdpr-worker/` | Мониторинг: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/monitoring/lib/queue_monitoring.cpp?rev=r8477996#L146</br>Тул: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/gdpr | Посмотреть логи gdpr-запросов, понять, почему они не обрабатываются
|`feedback-gdpr-requests-queue-max-age` | Возраст самого старого необработанного GDPR-запроса |  `/var/log/yandex/maps/feedback-gdpr-worker/` | Мониторинг: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/monitoring/lib/queue_monitoring.cpp?rev=r8477996#L164</br>Тул: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/gdpr | Найти в логах проблемный запрос и посмотреть, что ему мешает.
|`feedback-sync-tasks-queue` | Размер очереди задач синхронизации фидбека с другими сервисами (табличка `fbapi.sync_queue`) | `/var/log/yandex/maps/feedback-synchronization-tool/` | Мониторинг: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/monitoring/lib/queue_monitoring.cpp?rev=r8477996#L166</br>Тул: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/synctool | Найти в логах id проблемного фидбека и посмотреть, что ему мешает.
|`feedback-sync-tasks-queue-max-age` | Возраст самой старой необработанной задачи синхронизации фидбэка с другими сервисами (табличка `fbapi.sync_queue`)| `/var/log/yandex/maps/feedback-synchronization-tool/` | Мониторинг: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/monitoring/lib/queue_monitoring.cpp?rev=r8477996#L166.</br>Тул: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/synctool | Найти в логах id проблемного фидбека и посмотреть, что ему мешает.


##### Что делать с id проблемного фидбека

1. Посмотреть на данные можно в админке:
    - тестинг: https://feedback-admin.tst.c.maps.yandex-team.ru
    - прод: https://feedback-admin.c.maps.yandex-team.ru
2. Или посмотреть в бд: табличка `feedback_task`


##### Как потушить мониторинги

###### feedback-support-updater. err: Cannot update in progress tasks: Cannot get samsara tickets, status code = 403

[GEOMONITORINGS-14713](https://st.yandex-team.ru/GEOMONITORINGS-14713)

Кто-то унёс тикеты в закрытые очереди. И воркер не может их трекать.

Надо найти такие тикеты среди 50 id-шников из запроса:
```shell
#!/bin/bash

my_string="ticketId=114529729&ticketId=114602674&ticketId=114588370&ticketId=112996323&ticketId=117132458&ticketId=109175884&ticketId=115367755&ticketId=114433613&ticketId=117440998&ticketId=113472593&ticketId=114571439&ticketId=113154713&ticketId=113139807&ticketId=116034413&ticketId=113540128&ticketId=114360324&ticketId=112136399&ticketId=112509751&ticketId=114808779&ticketId=113796295&ticketId=115281556&ticketId=113579109&ticketId=113206377&ticketId=114546741&ticketId=116210678&ticketId=110382811&ticketId=113609997&ticketId=112129674&ticketId=114340069&ticketId=113120656&ticketId=119118786&ticketId=114343417&ticketId=114968670&ticketId=116780560&ticketId=117490161&ticketId=114207892&ticketId=114011230&ticketId=108805567&ticketId=114409087&ticketId=113524139&ticketId=116527748&ticketId=113154371&ticketId=113962313&ticketId=116463502&ticketId=114021140&ticketId=113917388&ticketId=113122941&ticketId=113102220&ticketId=109181386&ticketId=113472212"
cut_string=($(echo $my_string | sed "s/ticketId=//g"))
IFS='&' read -ra my_array <<< "$cut_string"

echo 'rm res'

#Print the split string
for i in "${my_array[@]}"
do
    echo 'echo -n "getting '$i'..." >> res'
    echo 'curl -H "Authorization: <АВТОРИЗАЦИЯ robot-wikimap>" "https://api.samsara.yandex-team.ru/api/v2/tickets/'$i'" | grep "ERROR" >> res'
    echo 'echo'
    echo 'sleep 0.1'
done

echo 'cat res | grep ERROR'
```
Запускать можно со ```spica```.

С найденными id-шниками надо идти к сапортам (@chdm), чтобы они принесли тикеты обратно.

P.S. Можно найти сразу все 'плохие' тикеты в базе.

**select_list.sql**
```sql
select string_agg(samsara_id::text, ',') as nnn from (
    select integration::jsonb->'services'->'support'->'service_object_id'::text as samsara_id
    from feedback_task
    where service = 'support'
    and status = 'in_progress'
) as lll;
```
Выполнять так:
```shell
GPASSWORD=******* psql --username extmaps_feedback_production --dbname maps_feedback_prod --port 6432 --host c-6f727507-606f-46a9-9ade-96ede15509d2.rw.db.yandex.net -f select_list.sql > list
```

#### Известные проблемы:
1. https://st.yandex-team.ru/MAPSHTTPAPI-1029

    Если организацию не получается найти в геопоиске, то мы не можем отправить нотификацию по ней, и удаляем нотификации из БД.
Организацию не получается найти, если например, она помечена как geospam в [altay](altay.yandex-team.ru).

   **Проблема**: пользователь зарепортил, что организация закрылась/некорректная. Его правку опубликовали, убрали организацию с карты. Пометили геоспамом в алтае. Данные не выгрузились в геопоиск, мы там не смогли её найти и отправить пользователю уведомление. В итоге теряем примерно 10 пушей в день.

2. https://st.yandex-team.ru/NMAPS-11640
  * ~~Сейчас не всегда из Сансары забираем нужные данные: в итоге наружу может попадать чувствительная информация.~~
  * ~~Сейчас синхронизируем не все тикеты, которые нужно: не трогаем closed тикеты со второй линии саппорта. Надо начать синхронизировать и их тоже, как описано в [воркфлоу](https://wiki.yandex-team.ru/users/echarzhova/Vorkflou-obrabotki-fidbeka/#vorkfloudljatiketovpostupivshixspervojjlinii).~~

3. Неправильно формируется ссылка на ui в алтале. Она не используется в админке, поэтому некритично.

## Как выкатить сервис
При выкатке нужно помнить про совместимость с [userapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/userapi). Для применения каких-то изменений может понадобиться выкатка обоих сервисов. Если нужно выкатить оба сервиса, то в каждом окружении сначала надо накатывать миграцию, а потом сервисы по очереди.

1. Выкатить миграцию в тестинг. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/migrations/README.md) по выкатке
2. Выкатить сервис в тестинг. [Документация sedem-а](https://docs.yandex-team.ru/sedem/releases)
3. Проверить, что работает отправка фидбека: на https://l7test.yandex.ru/maps отправить любой фидбек и найти его в админке: https://feedback-admin.tst.c.maps.yandex-team.ru
4. Иногда бывает нужно проверить, что работает синхронизация со справочником/сансарой/няк. Весь флоу обработки фидбека полностью совпадает с флоу в проде, поэтому можно явно прокликать нужные сценарии
5. Выкатить миграцию в прод. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/migrations/README.md) по выкатке
6. Выкатить сервис в прод

## Documentation

* Для авторизации нужен tvm.
   - tvm-id в тестинге: `2020773`
   - tvm-id в проде: `2020771`
* [Форматы](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas) запросов и ответов
* [Воркфлоу интеграции с саппортом](https://wiki.yandex-team.ru/users/echarzhova/Vorkflou-obrabotki-fidbeka/#vorkfloudljatiketovpostupivshixspervojjlinii)
* [Ручки фидбека](https://wiki.yandex-team.ru/sprav/api/feedback/#m-telozaprosa) со стороны Справочника. Если на стороне Справочника что-то пошло не так, можно спрашивать Сергея Соболя ( sobols@yandex-team.ru )
* [Документация по формам фидбека](https://a.yandex-team.ru/arc_vcs/maps/front/services/maps/docs/feedback.md)

## How to add new feedback type
1. Согласовать формат для нового типа фидбека. Основные заинтересованные сервисы - https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-feedback в лице miror@ и https://abc.yandex-team.ru/services/maps-front-feedback/ в лице kensora@.
2. Добавить новые значения `question_id` и `answer_id` в [libs/common/types.h](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/libs/common/types.h) и в [libs/common/types.сpp](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/libs/common/types.cpp)
3. Добавить эти значения в [константы](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/libs/common/validator.cpp) для валидации
4. Обновить схемы [question-context](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/question-context.json) и [answer-context](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/answer-context.json), если появился новый тип контекста
5. Обновить [документацию](https://a.yandex-team.ru/arc_vcs/maps/wikimap/feedback/docs/service/api.md)
6. Если требуется наличие centerPoint, добавить в [проверку](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/src/libs/common/validator.cpp?rev=r8057459#L127) новый тип.
7. Добавить значения в рассылку [email-ов](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/src/libs/dbqueries/notifications.cpp?rev=r8120740#L24).
8. Добавить новые ключи в [танкер](https://tanker-beta.yandex-team.ru/project/maps_feedback/keyset/UGCAccount). Проверить, что они корректно отображаются в [личном кабинете](https://l7test.yandex.by/maps/profile/ugc/feedback) после отправки фидбека в тестинге.

## Known clients
- [Админка фидбека](https://abc.yandex-team.ru/services/maps-front-feedback-admin)
- БЯК
- МЯК (https://github.yandex-team.ru/maps/mobmaps-proxy-api)
- [API личного кабинета](https://abc.yandex-team.ru/services/maps-front-user-account-int/)
- [sync_fbapi_feedback_worker](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_feedback/src/sync_fbapi_feedback_worker) из tasks_feedback
- [editor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/editor)
Для последних двух хосты прописаны в [конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/cfg/services/services.production.xml).


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FEEDBACK_API_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FEEDBACK_API_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FEEDBACK_API_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FEEDBACK_API_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations

Нет

## Полезные ссылки

* [Дашборд](https://datalens.yandex-team.ru/ywy6v7i0ywjyr-feedback-metrics)
* Процессы построения продуктовых метрик
   * Customer Satisfaction: [CSAT](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/feedback_csat/CSAT.md)
   * [Расчёт](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/fbapi_feedback_metrics) метрик
* [Инструкция](https://wiki.yandex-team.ru/users/abulich/pravila-moderacii-fidbjeka-i-gipotez) по разбору фидбека в НК

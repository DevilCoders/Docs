# Prod

## dsp_creative

Продовая инсталляция состоит из 5 "обычных" локаций и одной хамстерной.
В каждой локации развернуты собственные rs, rs proxy, shard и chunk controller-ы.
Локации независимы и управляются собственными shard и chunk controller-ами.
Устроены локации по-разному:
* sas, man, vla – по схеме сожительства YP с базовым, то есть, в кластерах базовых выделены группы,
  мощность которых слита в YP, и на этих мощностях подняты поды rs и rs proxy;
* myt и iva – обычный YP, при этом storage организован на hdd, а чанки поднимаются в память;
* sas-hamster – обычный YP, storage на ssd, чанки в память не поднимаются.

chunk-controller на prestable-контуре запущен [здесь.](https://deploy.yandex-team.ru/stages/chunk-controller)
Для реплика-сетов, обслуживаемых чанк-контроллером желательно иметь /labels/yd.deploy_policy = remove_delegation. Это даст возможность чанк-контроллеру делать разбор переезжающих подов.
Чанк-контроллер не порождает отдельные ендпойнтсеты для каждого чанка, а отдает клиентам топологии с парами (pod_id, endpoint_set_id). Здесь endpoint_set_id это enpoint_set, создаваемый deploy
для каждого replica_set по умолчанию. А значит, для того чтобы каждый чанк по отдельности оставался доступным необходимо выставлять для данного endpoint_set liveness_limit_ratio=1.

Каждая локация – это один stage
* [sas-saas2](https://deploy.yandex-team.ru/stages/sas-saas2)
* [man-saas2](https://deploy.yandex-team.ru/stages/man-saas2)
* [vla-saas2](https://deploy.yandex-team.ru/stages/vla-saas2)
* [iva-saas2](https://deploy.yandex-team.ru/stages/iva-saas2)
* [myt-saas2](https://deploy.yandex-team.ru/stages/myt-saas2)
* [sas-hamster-saas2](https://deploy.yandex-team.ru/stages/sas-hamster-saas2)

## banner_tier_main

Будущий прод для баннеров (c kvrs)
* coordinator запущен в [man-yabs-saas2](https://deploy.yandex-team.ru/stages/man-yabs-saas2)

### Deploy Stages

* [sas-yabs-saas2](https://deploy.yandex-team.ru/stages/sas-yabs-saas2)
* [man-yabs-saas2](https://deploy.yandex-team.ru/stages/man-yabs-saas2)
* [vla-yabs-saas2](https://deploy.yandex-team.ru/stages/vla-yabs-saas2)
* [sas-hamster2-saas2](https://deploy.yandex-team.ru/stages/sas-hamster2-saas2)

### Воркеры + GC
Тестинг (креативы + баннеры):
[saas2_test_worker](https://deploy.yandex-team.ru/projects/saas2_test_worker)  
Прод (креативы + баннеры):
[dsp_creative_worker](https://deploy.yandex-team.ru/projects/dsp_creative_worker)

### YT

[markov://home/saas2/prod/yabs](https://yt.yandex-team.ru/markov/navigation?path=//home/saas2/prod/yabs)

### Конфиги контроллеров
[search/plutonium/deploy/config](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/deploy/config)
* Префикс **yabs** - это файлы с шаблонами/конфигами для этой инсталяции
* Организован package для сборки всех конфигов в один архив, используется в coordinator и shardctrl

### Конфиги deployer'а
[Deployer 3.0 (C++)](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/deploy/agent/package)
* Организован package для сборки всех конфигов и бинаря деплоера в один архив, выкачен на баннерные стейджи

[Deployer 2.0 (python)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/deploy/deployer/package)
* Организован package для сборки всех конфигов и бинаря деплоера в один архив, выкачен на стейджи тестинг и хамстер креативов
Конфигов прода креативов в Аркадии нет

### Конфиги воркеров
[search/plutonium/workers/configs](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/workers/configs)
* Организован package для сборки всех конфигов в один архив, катится на все стейджи. Имя конфига соответствует имени стейджа

## Мониторинг
[Обзорная панель со всеми локациями (креативы)](https://yasm.yandex-team.ru/template/panel/saas-2.0-overview/)  
Панельки KVRS:  
[KVRS тестинг man-pre](https://yasm.yandex-team.ru/template/panel/saas2_kvrs/stage=test-saas2/)  
[KVRS хамстер (sas-hamster2-saas2)](https://yasm.yandex-team.ru/template/panel/saas2_kvrs/stage=sas-hamster2-saas2/)  
[KVRS SAS](https://yasm.yandex-team.ru/template/panel/saas2_kvrs/stage=sas-yabs-saas2/)  
[KVRS MAN](https://yasm.yandex-team.ru/template/panel/saas2_kvrs/stage=man-yabs-saas2/)  
[KVRS VLA](https://yasm.yandex-team.ru/template/panel/saas2_kvrs/stage=vla-yabs-saas2/)  

Состояние отдельно взятой локации удобно наблюдать на
[панели rs proxy](https://yasm.yandex-team.ru/template/panel/saas2_rsproxy/stage=sas-saas2/).
Во избежание нежелательного суммирования сигналов с разных стейджей
рекомендуется не пользоваться geo- и ctype-тегами, а явно указывать stage.

Доставку данных можно мониторить на
[панели с сигналами от воркера до деплоеров](https://yasm.yandex-team.ru/panel/okats._2CZOwu).

Есть отдельная [панель shard controller-a](https://yasm.yandex-team.ru/panel/mcden._LbBL1i?by=ctype).

[Сигналы чанк-контроллера](https://yasm.yandex-team.ru/chart/itype=callistoctrl;hosts=ASEARCH;ctype=prod;graphs=unistat-module_core_name_success_iteration_age_s_ammm,unistat-module_chunk_ctrl_name_sum_free_space_ammm,%7Bunistat-module_chunk_ctrl_name_failed_to_plan_ammm,unistat-module_chunk_ctrl_name_planned_ammm%7D,unistat-module_core_name_owns_lock_ammm/).
Отдаются только c активных реплик. 

* failed_to_plan -- количество поколений, которые не смогли распланироваться
* planned -- количество распланированных поколений

Также, чанк-контроллер пишет свой fqdn и время последней модификации состояния в yt в отдельную табличку. [Пример](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/saas2/prod/dsp_creative/ctrl/sas/modify_locks)

[Панель GC](https://yasm.yandex-team.ru/template/panel/saas2_gc/)
Аналогично чанк-контроллеру, сигналы отдаются только c активных реплик.

Панели воркера:
* [прод креативов](https://yasm.yandex-team.ru/template/panel/saas2_worker/stage=saas2-prod-dsp_creative-worker;deploy_unit=deployUnit/)
* [prod banner_tier_main(цари)](https://yasm.yandex-team.ru/template/panel/saas2_worker/stage=saas2-prod-dsp_creative-worker;deploy_unit=banner_tier_main/)
* [prod banner_resources (по состоянию на 29.12.2021 не запущены)](https://yasm.yandex-team.ru/template/panel/saas2_worker/stage=saas2-prod-dsp_creative-worker;deploy_unit=banner_resources/)

Панели очередей Цезаря:
* [Prod-очередь dsp_creatives](https://solomon.yandex-team.ru/?project=big_rt_queue_daemon&dashboard=queue_lags_and_rate&cluster=markov&l.consumer=saas_stable&l.queue=%2F%2Fhome%2Fbigb%2Fcaesar%2Fstable%2FDspCreativesUpdatedKeys&b=1w&e=)
* [Prestable-очередь dsp_creatives](https://solomon.yandex-team.ru/?project=big_rt_queue_daemon&dashboard=queue_lags_and_rate&cluster=markov&l.consumer=saas_prestable&l.queue=%2F%2Fhome%2Fbigb%2Fcaesar%2Fprestable%2FDspCreativesUpdatedKeys&b=1w&e=)
* [Prod-очередь banner_tier_main](https://solomon.yandex-team.ru/?project=big_rt_queue_daemon&dashboard=queue_lags_and_rate&cluster=markov&l.consumer=saas_stable_tier_main&l.queue=%2F%2Fhome%2Fbigb%2Fcaesar%2Fstable%2FBannersUpdatedKeys&b=3d12h&e=)
* [Prestable-очередь banner_tier_main](https://solomon.yandex-team.ru/?project=big_rt_queue_daemon&dashboard=queue_lags_and_rate&cluster=markov&l.consumer=saas_prestable&l.queue=%2F%2Fhome%2Fbigb%2Fcaesar%2Fprestable%2FBannersUpdatedKeys&b=1w&e=)

## Алерты

Шаблоны алертов, а также шаблоны панелей Голована, [закоммичены в Аркадию](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/yasm_templates/), каждому файлику соответствует одноименный шаблон алертов. Катится через CI, подробнее в [readme](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/yasm_templates/readme.md)

Чанк-контроллер:  
[Количество поколений чанков, которые не вышло распланировать](https://yasm.yandex-team.ru/alert/saas2-failed-to-plan)  
[Возраст последней успешной итерации чанк-контроллера](https://yasm.yandex-team.ru/alert/saas2-chunk-ctrl-iteration-age)  

[Алерты в Соломоне](https://solomon.yandex-team.ru/admin/projects/saas2/alerts)  
[Правило в Juggler'е к алертам в Соломоне](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=606700624524dd00d7c0f9fa)

## Релизы
[Ссылка на проект в CI](https://a.yandex-team.ru/projects/saas2/ci)  
По состоянию на 29.12.2021 настроены релизы чанк-контроллера, деплоера 2.0 и 3.0, агента GC и его конфигов, шард-контроллера, воркера и его конфигов, шаблонов панелей и алертов в Головане. Релизы чанк-контроллера и шард-контроллера на прод катятся ручным подтверждением тикета в соответствующем стейдже Деплоя.

Для остальных сервисов интеграции нет, релизы ручные.

## Дежурства
На текущий момент в ротации участвуют только активные разработчики saas 2.0.
В дежурную смену ничего не отдано.

[Календарь дежурств](https://abc.yandex-team.ru/services/saas2/duty/)


# Prestable

## Deploy

### Воркеры
[worker+gc, общий для контуров kvrs и rsproxy](https://deploy.yandex-team.ru/projects/saas2_test_worker)

### Контур kvrs
[coordinator, shardctrl, chunkctrl](https://deploy.yandex-team.ru/stages/test-saas2)  
[bk_stat, kvrs](https://man-pre.deploy.yandex-team.ru/stages/test-saas2)

### Контур rs + rsproxy
[coordinator, shardctrl, rsproxy](https://man-pre.deploy.yandex-team.ru/stages/rs-proxy)  
[rs](https://man-pre.deploy.yandex-team.ru/stages/remote-storage)  
[chunkctrl](https://deploy.yandex-team.ru/projects/ssmike)  

## YT
[arnold://home/saas2/plutonium/yaps/man-pre/testing](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas2/plutonium/yaps/man-pre/testing)

## Конфиги
[search/plutonium/deploy/config](https://a.yandex-team.ru/arc/trunk/arcadia/search/plutonium/deploy/config)
* Перфикс **man-pre** - контур rs + rsproxy, например, dsp_creative
* Перфикс **test-saas2** - контур kvrs, например, banner_tier_main

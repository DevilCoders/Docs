# Nanny

## Введение {#intro}

Мы стараемся сделать переезд из nanny в deploy как можно проще и более автоматизированно.
Текущая версия мигрирует nanny service в deploy.

Не все фичи nanny поддержаны. Чтобы узнать покрытие вашего сервиса, пройдите по инструкции ниже.
Вопросы можно задавать в [чат rtc-support](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q) или очередь [RTCSUPPORT](https://st.yandex-team.ru/createTicket?queue=RTCSUPPORT).

Инструкция использует [dctl](../../reference/tools/dctl.md) (консольный тул) в качестве интерфейса к Deploy.

Покрытие фичей Deploy в dctl выше, чем в UI.
Если вы пользуетесь фичами, не покрытыми UI, вы не сможете редактировать stage через UI (но сможете на него смотреть).

## Миграция квот {#quota_migration}

Для того, чтобы запустить ваш сервис в Y.Deploy, вам нужна квота в YP (подробнее про квоты в YP). Квота в YP выдается на ABC-сервис. Далее возможны следующие опции:

1. У вашего сервиса уже есть необходимая квота в YP (например, вы живете в YP.Lite). В этом случае все просто: вам нужно указать этот ABC-сервис в качестве источника квоты при создании проекта в Y.Deploy.
1. У вас нет необходимой квоты в YP, но есть квота в gencfg - воспользуйтесь [инструкцией](https://wiki.yandex-team.ru/yp/instrukcija-po-pereezdu-gencfg-yp/#perenestikvotyizgensfgvyp) по миграции квот.
1. У вас нет необходимой квоты в YP. Тогда вам нужно запросить квоту через ABC.
1. Если ваша цель просто попробовать Y.Deploy (чтобы разобраться как устроена система), вы можете воспользоваться [временной (tmp) квотой](https://wiki.yandex-team.ru/yp/tmp/). **Мы категорически против использования tmp-квоты для запуска продакшен сервиса**. Кроме того, в рамках tmp-квоты вы **не сможете запустить балансер в AWACS**.

## Инструкция по миграции сервиса {#service_migration}

* Обновите [ya tool](https://wiki.yandex-team.ru/yatool/distrib/).
* Запустить `ya tool yd-migrate dump_nanny`

Этот тул:
* прочитает описание service из nanny
* прочитает описание YP.Lite подов из YP
* по необходимости скачает instancectl.conf/loop.conf из sandbox
* запишет спеку deploy stage в файл ./deploy.yaml

Токен няни можно получить тут: [https://nanny.yandex-team.ru/ui/#/oauth/](https://nanny.yandex-team.ru/ui/#/oauth/)

Токен YP можно получить тут: [https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7)

Некоторые фичи вашего сервиса могли не смигрироваться. Читайте warning логи.

```bash
/# подробный список аргументов смотрите в ya tool yd-migrate dump_nanny -h
danibw@danibw-dev1:~/arcadia$ ya tool yd-migrate dump_nanny <NANNY_TOKEN> <YP_TOKEN> test_danibw_hello_word
2020-07-10 14:12:11 | root                 | W | Assuming that instance layers contain symlinks needed for bind_skynet ( https://wiki.yandex-team.ru/ru/podstack/box/#bindskynet )
2020-07-10 14:12:12 | root                 | I | ['ssh', u'test-danibw-hello-word-1.sas.yp-c.yandex.net', 'ls nanny_vault']
2020-07-10 14:12:16 | root                 | I | ['ssh', u'test-danibw-hello-word-1.sas.yp-c.yandex.net', 'cat nanny_vault/test_key']
2020-07-10 14:12:18 | root                 | W | Secret ACL (for users/abc services) werent migrated - secret is only available for you and stage instances.
2020-07-10 14:12:18 | root                 | W | Please, update yav ACL manually at https://yav.yandex-team.ru/secret/sec-01ecw6t4d52ryfeq9dq87q5s6h
2020-07-10 14:12:19 | root                 | I | ['ssh', u'test-danibw-hello-word-1.sas.yp-c.yandex.net', 'cat /proc/$(cat pids/test_danibw_hello_word-1)/environ']
2020-07-10 14:12:21 | root                 | W | Secret ACL (for users/abc services) werent migrated - secret is only available for you and stage instances.
2020-07-10 14:12:21 | root                 | W | Please, update yav ACL manually at https://yav.yandex-team.ru/secret/sec-01ecw6t79pmqxen6jc15k03pht
2020-07-10 14:12:22 | root                 | W | Multiple disk_volume_requests are not supported at YD yet, will sum up all disk qouta at one volume
2020-07-10 14:12:22 | root                 | W | Resource 1198993879 will be placed in /SAMOGON_BUNDLE. Please, reconfigure your application.
2020-07-10 14:12:22 | root                 | W | Your static_files will be at /static_files. Please, reconfigure your application.
2020-07-10 14:12:22 | root                 | W | NOT_IMPLEMENTED: field = '[{u'srcPath': u'config_template.yaml', u'dstPath': u'config.yaml'}]', supported only [[]] at [u'runtime_attrs', u'content', u'instance_spec', u'volume', 0, u'templateVolume', u'template']
2020-07-10 14:12:22 | root                 | W | NOT_IMPLEMENTED: field = 'logic_or', supported only [] at [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'active_checks', 0, u'module', u'type']
2020-07-10 14:12:22 | root                 | W | field [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'active_checks', 0, u'module', u'logic_or'] is not at IMPLEMENTED_MAP at [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'active_checks', 0, u'module', u'logic_or']
2020-07-10 14:12:22 | root                 | W | NOT_IMPLEMENTED: field = 'test_danibw_hw_check', supported only [''] at [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'active_checks', 0, u'passive_checks', 0, u'juggler_service_name']
2020-07-10 14:12:22 | root                 | W | field [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'juggler_hosts', 0, u'golem_responsible'] is not at IMPLEMENTED_MAP at [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'juggler_hosts', 0, u'golem_responsible']
2020-07-10 14:12:22 | root                 | W | field [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'juggler_hosts', 0, u'name'] is not at IMPLEMENTED_MAP at [u'info_attrs', u'content', u'monitoring_settings', u'juggler_settings', u'content', u'juggler_hosts', 0, u'name']
2020-07-10 14:12:22 | root                 | I | check stage.yaml (nanny service -> YD.stage) and run `ya tool dctl put stage stage.yaml` when ready
2020-07-10 14:12:22 | root                 | I | This logs are also available at yd_migrate.log
```

* Записать deploy.yaml в Deploy

Предварительно можете внести дополнительные правки руками (имя stage/deploy_unit в deploy.yaml менять нельзя - под него выписался delegation token для секретов)

```bash
danibw@danibw-dev1:~/arcadia$ ya tool dctl put stage stage.yaml
Put stage: test_danibw_hello_word
```

* (optional) Переконфигурируйте ваши балансеры (или других клиентов вашего сервиса)
Service discovery устроен через YP endpoint_set (так же, как в YP.Lite).
* (optional) Если есть секреты из nanny vault, обновить соответствующие yav acl (см. ссылки в логах)

## Подсчет покрытия проекта (множества сервисов) {#service_list_coverage}

В Аркадии лежит скрипт, который считает покрытие мигратором заданного списка сервисов, он выводит:

- список "готовых к миграции" сервисов - все фичи которых уже поддержаны
- список непокрытых мигратором фичей, упорядоченных по количеству сервисов, в которых фича используется

Пример использования:

```bash
# собрать бинарь
yanddmi@yanddmi-dev[~/arcadia/infra/deploy/tools/yd_migrate/bin/nanny_coverage]:ya make --yt-store
Ok

# формат списка сервисов:
yanddmi@yanddmi-dev[~/arcadia/infra/deploy/tools/yd_migrate/bin/nanny_coverage]:head market_filter.txt 
prod_market_light_matcher_sas
prod_market_clutcher_sas
production_market_static_pages_msk
prod_market_matcher_iva
prod_market_matcher_general_sas

# загрузка описания сервисов из няни в файл nanny_market.json
# выключенные - offline - сервисы игнорируются
yanddmi@yanddmi-dev[~/arcadia/infra/deploy/tools/yd_migrate/bin/nanny_coverage]:./feature_coverage -d nanny_market.json dump <nanny_token> -c service_list.txt 
urllib3.connectionpo | D | Starting new HTTP connection (1): nanny.yandex-team.ru:80
urllib3.connectionpo | D | http://nanny.yandex-team.ru:80 "GET /v2/services/?limit=100&skip=0 HTTP/1.1" 200 214220
urllib3.connectionpo | D | http://nanny.yandex-team.ru:80 "GET /v2/services/?limit=100&skip=100 HTTP/1.1" 200 164509
urllib3.connectionpo | D | http://nanny.yandex-team.ru:80 "GET /v2/services/?limit=100&skip=200 HTTP/1.1" 200 462290
root                 | I | found service adv-machine-online-beru-machine
root                 | I | found service adv-machine-online-merch-machine
...
urllib3.connectionpo | D | http://nanny.yandex-team.ru:80 "GET /v2/services/?limit=100&skip=19300 HTTP/1.1" 200 82184
urllib3.connectionpo | D | http://nanny.yandex-team.ru:80 "GET /v2/services/?limit=100&skip=19313 HTTP/1.1" 200 13
root                 | I | total services: 1862

# подсчет покрытия сервисов из nanny_market.json
yanddmi@yanddmi-dev[~/arcadia/infra/deploy/tools/yd_migrate/bin/nanny_coverage]:./feature_coverage -d nanny_market.json calc 
root                 | D | ready_for_migrate: ["production_market_pricechart_info_iva", "testing_market_abo_main_sas", "testing_market_autogeneration_api_vla", ..., "testing_market_mbo_react_ui_sas", "testing_market_checkout_push_api_load_sas", "production_market_fulfillment_workflow_api_vla"]
root                 | I | total specs: 1862
root                 | I | ready_for_migrate: 216 (11%)
root                 | I | %     : percentage of services, that would be ready for migration after implementation of this feature, and all on top of it
root                 | I | CNT   : number of services, that would be ready for migration after implementation of this feature, and all on top of it
root                 | I | USAGE : number of services, that use this feature
root                 | I | ready_on_prefix_implementation:     
  %   CNT USAGE FEATURE    
 11   216   818 runtime_attrs/content/instance_spec/volume/X/secretVolume/keychainSecret/keychainId    
 11   216   818 runtime_attrs/content/instance_spec/volume/X/secretVolume/keychainSecret/secretRevisionId    
 18   352   818 runtime_attrs/content/instance_spec/volume/X/secretVolume/keychainSecret/secretId    
 34   641   816 runtime_attrs/content/instance_spec/networkProperties/etcHosts/SET_HOSTNAME    
 45   843   791 runtime_attrs/content/resources/sandbox_files/X/is_dynamic    
 45   843   475 runtime_attrs/content/instance_spec/notifyAction/handlers/X/type/EXEC    
 53   991   475 runtime_attrs/content/instance_spec/notifyAction/handlers/X/execAction/command    
 53   991   314 runtime_attrs/content/instance_spec/containers/X/coredumpPolicy/coredumpProcessor/totalSizeLimit    
 53   991   309 runtime_attrs/content/instance_spec/containers/X/coredumpPolicy/coredumpProcessor/countLimit    
 53   992   299 runtime_attrs/content/instance_spec/containers/X/coredumpPolicy/type/COREDUMP
 ...
```

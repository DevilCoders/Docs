# Использование мигратора

Мы стараемся сделать переезд из qloud в deploy как можно проще и более автоматизированно.
Текущая версия мигрирует qloud.environment в тройку:

- deploy.[stage](../../../concepts/stage/stage.md): все, что связано с "бекендами"
- [awacs](https://wiki.yandex-team.ru/cplb/awacs/).namespace: все, что связано с балансировкой (включая upstreams)
- [yav](https://vault-api.passport.yandex.net/docs/).secret: секреты

Не все фичи qloud поддержаны. Чтобы узнать покрытие вашего environment, пройдите по инструкции ниже.
Вопросы можно задавать в [чат rtc-support](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q) или очередь [RTCSUPPORT](https://st.yandex-team.ru/createTicket?queue=RTCSUPPORT).

Инструкция использует [dctl](../../../reference/tools/dctl.md) (консольный тул) в качестве интерфейса к Deploy.

Покрытие фичей Deploy в dctl выше, чем в UI.
Если вы пользуетесь фичами, не покрытыми UI, вы не сможете редактировать stage через UI (но сможете на него смотреть).
Это будет устраняться в процессе разработки UI. DEPLOY-1699

[Инструкция по миграции квот](quota.md)

## Инструкция по миграции окружения {#environment_migration}

* Обновите [ya tool](https://wiki.yandex-team.ru/yatool/distrib/).
* Запустить `ya tool yd-migrate dump_qloud`

Этот тул:

* прочитает описание environment из qloud.
* сходит по ssh в инстанс за значениями секретов
* запишет секреты в yav под указанным алиасом, выпишет для них delegation_token на указанный stage-id
* запишет спеку deploy stage в файл ./deploy.yaml
* запишет спеку [awacs](https://wiki.yandex-team.ru/cplb/awacs/) balancer в файл ./awacs.yaml

Некоторые фичи вашего environment могли не смигрироваться. Читайте warning логи.

```bash
/# подробный список аргументов смотрите в ya tool yd-migrate dump_qloud -h
yanddmi@yanddmi-dev:ya tool yd-migrate dump_qloud platform samogon yanddmitest0 simplehttpserver 1040 svc_myservice_administration \
--stage-id simplehttpserver \
--awacs-category users/yanddmi \
--awacs-namespace-id simplehttpserver \
--yav-secret-alias simplehttpserver
root                 | I | SKIP: field ['domains', 0, u'type']
root                 | I | Running ['ssh', u'man4-be8b92e8d7a6.qloud-c.yandex.net', u'cat /secret/override-yanddmi-test-bin-file']
root                 | I | Running ['ssh', u'man4-be8b92e8d7a6.qloud-c.yandex.net', 'cat /proc/$(pidof qloud-init)/environ']
root                 | W | Secret ACL werent migrated. Please, update yav ACL manually at https://yav.yandex-team.ru/secret/sec-01dhnpx1t7eahavh43dazfjqm9
root                 | W | TVM client port is 2 at Y.Deploy (not 1 as in Qloud). Please, update your application to use $DEPLOY_TVM_TOOL_URL env.
root                 | W | TVM client token is at $TVMTOOL_LOCAL_AUTHTOKEN at Y.Deploy (not at $QLOUD_TVM_TOKEN as in Qloud). Please, update your application.
root                 | I | SKIP: field ['dump', u'components', 0, u'activateRecipe', u'doneThreshold']
root                 | I | SKIP: field ['dump', u'components', 0, u'activateRecipe', u'updateLimit']
root                 | I | SKIP: field ['dump', u'components', 0, u'activateRecipe', u'updatePeriod']
root                 | I | SKIP: field ['dump', u'components', 0, u'properties', u'size', 'network'] = 16
root                 | I | check deploy.yaml (qloud components -> YD.stage) and run `ya tool dctl put stage deploy.yaml` when ready
root                 | I | check awacs.yaml (qloud domains/routes -> awacs namespace) and run `ya tool yd-migrate push_awacs <awacs_token>` when ready
```

* Записать deploy.yaml в Deploy
Предварительно можете внести дополнительные правки руками (имя stage/deploy_unit в deploy.yaml менять нельзя - под него выписался delegation token для секретов)

```bash
yanddmi@yanddmi-dev:ya tool dctl put stage deploy.yaml 
Put stage: simplehttpserver
```

* (optional) Записать awacs.yaml в Awacs
Команда создает/перезаписывает конфигурацию балансеров в awacs (включая создание namespace, если его не было).
Если у вас уже есть балансер в awacs, и вы хотите просто дописать в него domains/routes, не используйте эту команду: поправьте конфигурацию балансера в интерфейса awacs, взяв нужный кусок из awacs.yaml.  
Предварительно можете поправить имя namespace в awacs.yaml и внести дополнительные правки.  
В качестве получателя алертов в созданном namespace будет задан сервис или роль, указанные при запуске команды dump_qloud (**svc_myservice_administration** в примере выше).  
Как получить токен: [https://wiki.yandex-team.ru/cplb/awacs/api/#avtorizacija](https://wiki.yandex-team.ru/cplb/awacs/api/#avtorizacija)

```bash
yanddmi@yanddmi-dev:ya tool yd-migrate push_awacs <awacs_token>
root                 | I | Namespace "simplehttpserver" already exists. Skipping namespace creation.
root                 | I | Check your namespace at https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/simplehttpserver/show/
...
```

* (optional) Заведите l3 балансер
В интерфейсе awacs.
Инструкция: [https://wiki.yandex-team.ru/cplb/awacs/tutorial/L3-L7/#sozdaniel3-balansera](https://wiki.yandex-team.ru/cplb/awacs/tutorial/L3-L7/#sozdaniel3-balansera)

* (optional) Обновить dns records
Ни qloud, ни awacs, не владеют dns записями.
Поэтому изменения в [https://dns.tt.yandex-team.ru/request](https://dns.tt.yandex-team.ru/request) надо внести вручную.
Инструкция: [https://wiki.yandex-team.ru/cplb/awacs/tutorial/L3-L7/#dns](https://wiki.yandex-team.ru/cplb/awacs/tutorial/L3-L7/#dns)

* (optional) Мигрировать ip4-pool'ы
Документация по добавлению ip4-пула в YP: [https://wiki.yandex-team.ru/users/elshiko/kak-dobavit-novyjj-pul/](https://wiki.yandex-team.ru/users/elshiko/kak-dobavit-novyjj-pul/)

## Таблица маппинга сущностей {#entity_mapping}

В таблице указаны не все сущности, поддержанные мигратором

**Qloud** | **Deploy** | **комментарий**  
--- | --- | ---  
environment | stage + awacs.namespace + yav.secret | инстансы запускаются в deploy, балансировка настраивается в awacs, секреты в yav  
environment.component | stage.deploy_unit|  
environment.component.embedJugglerClient | stage.deploy_unit.box_juggler_configs | https://wiki.yandex-team.ru/ru/Sidecars/jugglersubagent/  
environment.component.environmentVariables | stage.deploy_unit.pod_spec.workload.env |  
environment.component.prepareRecipe | - | пока не поддерживается (дефолтные значения не считаются ошибкой при генерации спеки stage)  
environment.component.secrets | yav.secret | секреты мигрируются, только если указан ключ --yav-secret-alias. значения секретов достаются путем ssh-похода на один из инстасов. ACL не мигрируются  
environment.component.tvmConfig | stage.deploy_unit.tvm_config + yav.secret | client port 2 (не 1 как в Qloud), client token в $TVMTOOL_LOCAL_AUTHTOKEN (не в $QLOUD_TVM_TOKEN как в Qloud) https://wiki.yandex-team.ru/ru/sidecars/tvmtool/  
environment.routeSettings | awacs.namespace.upstream |  
environment.domains | awacs.namespace.domain | в awacs будет выпущен новый сертификат для того же домена - поддерживается только для YandexInternalCA  
balancer | awacs.namespace.<balancers_per_cluster> | l7 балансер - в awacs "распилен" на несколько инсталляций - per cluster 

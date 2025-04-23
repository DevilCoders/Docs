Утилита для автоматизации типичных операций MarketSRE CLI
=========================================================


Посмотреть информацию о сервисах
--------------------------------

Посмотреть текущее состояние сервисов:
```
$ ./marketsre nanny services --filter '^production_market_clickdaemon*' curstate
ONLINE    2020-05-28T12:05:41 https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_clickdaemon_vla
ONLINE    2020-05-28T12:07:34 https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_clickdaemon_sas
ONLINE    2020-05-28T12:05:19 https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_clickdaemon_iva
```

Найти сервисы, уже минимум 60 дней находящиейся не в ONLINE статусе, исключив при этом мультитестинги:
```
$ ./marketsre nanny services --category-exclude "/market/multitesting" curstate --state-age 60 --state-exclude "^ONLINE"
UPDATING  2020-03-30T11:12:50 https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_stock_storage_load_vla
OFFLINE   2019-10-08T17:05:38 https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_mbi_qa_sas
UPDATING  2020-06-29T17:06:27 https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_stock_storage_load_iva
OFFLINE   2020-06-02T12:06:52 https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_template_service_for_nodejs_vla
```

Посмотреть на инстансы сервисов, на их ip и project id.
```
./marketsre nanny services --category /market/report/goods/warehouse/ --category-exclude /market/multitesting show_instances --help
Usage: marketsre nanny services show_instances [OPTIONS]

  Show instances for nanny services.

Options:
  --show-host  show bare metal server
  --show-ip    show container ip
  --show-pid   show container project id
  --help       Show this message and exit.

/marketsre nanny services --category /market/report/goods/warehouse/ --category-exclude /market/multitesting show_instances --show-host --show-ip --show-pid

prod_report_goods_warehouse_man man0-9462-71e-man-market-prod--414-17058.gencfg-c.yandex.net man0-9462.search.yandex.net 2a02:6b8:c1a:2639:10f:28:0:42a2 0x10f0028
prod_report_goods_warehouse_man man0-9463-4ca-man-market-prod--414-17058.gencfg-c.yandex.net man0-9463.search.yandex.net 2a02:6b8:c1a:24b6:10f:28:0:42a2 0x10f0028
prod_report_goods_warehouse_man man0-9459-ca0-man-market-prod--414-17050.gencfg-c.yandex.net man0-9459.search.yandex.net 2a02:6b8:c1a:2fb6:10f:28:0:429a 0x10f0028
...
```
Можно не выводить bare metal host, ip или pid и/при желании.

Перезапуск всех инстансов фронта
--------------------------------

В случае, когда фронт после долгого закрытия ДЦ отваливается от кэша,
его нужно перезапустить вручную. Для этого была добавлена команда,
перезапускает ВСЕ инстансы заданного няня-сервиса параллельно.

Сервисы фронта:

- production_market_front_desktop_sas
- production_market_front_desktop_canary_sas
- production_market_front_desktop_vla
- production_market_front_desktop_canary_vla
- production_market_front_desktop_iva

- production_market_front_touch_sas
- production_market_front_touch_canary_sas
- production_market_front_touch_vla
- production_market_front_touch_canary_vla
- production_market_front_touch_iva

- production_market_front_blue_desktop_sas
- production_market_front_blue_desktop_vla
- production_market_front_blue_desktop_iva
- production_market_front_blue_desktop_canary_vla
- production_market_front_blue_desktop_canary_iva

- production_market_front_blue_touch_sas
- production_market_front_blue_touch_vla
- production_market_front_blue_touch_iva
- production_market_front_blue_touch_canary_vla
- production_market_front_blue_touch_canary_iva

Использование:

    ~/repos/arc/arcadia/market/sre $ tools/marketsre_cli/marketsre nanny service production_market_front_touch_sas force_restart
    200 OK
    {"message":"State applied"}
    ...
    20660@sas1-9969.search.yandex.net PREPARED
    20660@sas2-1261.search.yandex.net PREPARED
    200 OK
    {"message":"State applied"}
    ...
    20660@sas1-9969.search.yandex.net ACTIVE
    20660@sas2-1261.search.yandex.net ACTIVE


Обновление слоёв в сервисах
---------------------------

Посмотреть сервисы:

    pashayelkin@pashayelkin:~/repos/arc/arcadia/market/sre/tools/marketsre_cli (updatelayers)$ ./marketsre nanny services --filter testing_market_front show | grep -v mt_
    testing_market_front_vendors_sas
    testing_market_front_affiliate_sas
    testing_market_front_affiliate_vla
    ...

Посмотреть слои в одном сервисе:

    pashayelkin@pashayelkin:~/repos/arc/arcadia/market/sre/tools/marketsre_cli (updatelayers)$ ./marketsre nanny service testing_market_tsum_tms_man  layers show
    BUILD_PORTO_LAYER: 267288486 PORTO_LAYER_SEARCH_UBUNTU_TRUSTY: 603632582
    BUILD_PORTO_LAYER: 310548904 PORTO_LAYER_MARKET_BASE_TRUSTY: 697045791
    BUILD_PORTO_LAYER: 310560705 PORTO_LAYER_MARKET_JDK: 697071853

Посмотреть слои в нескольких сервисах:

    pashayelkin@pashayelkin:~/repos/arc/arcadia/market/sre/tools/marketsre_cli (updatelayers)$ ./marketsre nanny services --filter testing_market_tsum_tms  layers show
    testing_market_tsum_tms_vla
    testing_market_tsum_tms_man
    Layers:
        BUILD_PORTO_LAYER: 267288486 PORTO_LAYER_SEARCH_UBUNTU_TRUSTY: 603632582
        BUILD_PORTO_LAYER: 310548904 PORTO_LAYER_MARKET_BASE_TRUSTY: 697045791
        BUILD_PORTO_LAYER: 310560705 PORTO_LAYER_MARKET_JDK: 697071853
    Services:
        testing_market_tsum_tms_vla
        testing_market_tsum_tms_man

Обновить слои в одном сервисе:

    pashayelkin@pashayelkin:~/repos/arc/arcadia/market/sre/tools/marketsre_cli (updatelayers)$ ./marketsre nanny service  testing_market_front_desktop_load_sas  layers replace --comment 'CSADMIN-19528: Обновить Nginx в базовом образе до версии 1.14' 566424672  567404944
    Updated layers:
    <diff>
    Commit updated layers to nanny? [y/N]: y
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_load_sas/

Обновить слои в нескольких сервисах:

    pashayelkin@pashayelkin:~/repos/arc/arcadia/market/sre/tools/marketsre_cli (updatelayers)$ ./marketsre nanny services --filter testing_market_front_desktop layers replace --comment 'CSADMIN-19528: Обновить Nginx в базовом образе до версии 1.14' 566424672 567404944
    Services:
        testing_market_front_desktop_market_test_vla
        testing_market_front_desktop_market_test_sas
        testing_market_front_desktop_market_cached_sas
        testing_market_front_desktop_market_preview_sas
        testing_market_front_desktop_market_testing_sas
        testing_market_front_desktop_market_preview_vla
        testing_market_front_desktop_market_testing_vla
        testing_market_front_desktop_load_sample_sas
    New layers:
    BUILD_PORTO_LAYER: 566424672 PORTO_LAYER_MARKET_BASE_TRUSTY: 1253160242
    BUILD_PORTO_LAYER: 567404944 PORTO_LAYER_MARKET_NODEJS: 1255415705
    Update? [y/N]: y
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_market_test_vla/
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_market_test_sas/
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_market_cached_sas/
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_market_preview_sas/
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_market_testing_sas/
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_market_preview_vla/
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_market_testing_vla/
    Layers updated: https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_desktop_load_sample_sas/

Массовое обновления топологии gencfg:
-------------------------------------

Выполняется так:

    ./marketsre nanny services --filter 'testing_cs_dashboard_vla' update_gencfg_release --comment 'Test tool' stable-146-r1851

Добавление ключа `--force-downgrade` обновить тег gencfg, даже если он будет ниже текущей. Ключ `--activate` сразу активирует снапшот.

Добавление вольюмов (в том числе секретов) в InstancesSpec:
----------------------------------------------------------

Пример:

	./marketsre_cli nanny services --filter 'testing_cs_dashboard_vla' add_volume --volume-name push-client-tvm-secret-health --volume-type yav --secret-uuid sec-01dq7mnes1n6rq2mh7zn53n8ws --secret-version ver-01dq7mneytmhjcm8dgcagcdvs4

В результате в InstanceSpec создастся вольюм, который реализуется в контейнере в виде папочки `push-client-tvm-secret-health`, в которой будут размещены файлики с именами ключей из секретницы и содержимым секрета по этим же ключам. На текущий момент поддерживается только один тип вольюмов - для секретницы. По умолчанию токен для доступа к секрету пропишется c tvm-client-id от Nanny.

Отзыв токенов для Nanny сервисов
--------------------------------

При отзыве токенов используется немного извернутая логика. Мы в параметрах указываем секрет, а список сервиов, для которых отзываются токены для конкретного секрета задаются через параметры `--filter` и `--category`.

В этом случае произойдет следующее:

1. Скрипт выгрузит список всех токенов из секретницы (page-size установлен в 10000, и пока проверяется только для нее)
2. Сформирует список на удаление, выбрав из списка токенов только те, signature для которых является множество имен няне-сервисов, совпадающими в условиях `filter`.
3. Отзовет выбранные токены.

Логика в скрипте очень простая, не ожидайте от него интеллекта.

Пример использования:

	 ./marketsre nanny services --filter 'testing_cs_dashboard_.*' revoke_tokens --secret-uuid sec-01dq7mnes1n6rq2mh7zn53n8ws

Замена delegation-токена, который был ошибочно скопирован из шаблона в СПОК-е
-----------------------------------------------------------------------------

Пример:

	$ ./marketsre nanny services --filter 'production_cs_dashboard_.*' replace_vault_tokens --volume-name push-client-tvm-secret-health
	Volume push-client-tvm-secret-health will add to production_cs_dashboard_sas for rewriting token...
	Volume push-client-tvm-secret-health will add to production_cs_dashboard_vla for rewriting token...

	Will be rewrite tokens for next secrets:
		https://yav.yandex-team.ru/secret/sec-01dq7mnes1n6rq2mh7zn53n8ws
		https://yav.yandex-team.ru/secret/sec-01dq7mqadyn9rr9a4va6j4ehzh

	Do you want to rewrite tokens? [y/N]: y
	Service production_cs_dashboard_sas was updated
	Service production_cs_dashboard_vla was updated

`replace_vault_token` не отзывает предыдущий токен. Он просто выписывает новый и заменяет его на уже существующий в вольюме с именем из параметра `--volume-name`. Если такого вольюма нет, то он просто пропустит этот сервис в няне. Для добавления нового вольюма с секретом из секретницы используйте `add_volume`. Для отзыва старых токенов воспользуйтесь аргументом `revoke_tokens`.


Вывести все сервисы, где текущий ресурс больше/меньше требуемой версии
---------------------------------------------------------------------------

Аргумент `--show-rule` ожидает на входе один из 7 возможных вариантов и позволяет вывести список сервисов, где:

- `lt` или less than (текущий ресурс ниже необходимой версии)
- `lte` или less than or equal (текущий ресурс ниже или равен необходимому)
- `gt` или great than (текущий ресурсы выше необходимой версии)
- `gte` или great than or equal (текущий ресурс выше или равен необходимому)
- `eq` или strong equal (текущий ресурс равен необходимому)
- `ne` или not equal (текущий ресурс не равен необходимому)
- `all` или all (все ресурсы)

Если текущий ресурс ниже необходимого ресурса, вывод будет красной строчкой, если равен - то синей, если выше, то зеленой. Вывод группируется по результату (больше/меньше версия), и соответственно по цвету.

Пример:

```
./marketsre nanny services --filter 'testing_market_front_.*' check_resource_version --resource-type STATBOX_PUSHCLIENT --need-resource-id 1701136678 --show-rule all

  [####################################]  100%

~~~ Services where current resource id is equal need resource id: ~~~

testing_market_front_desktop_sas current=1701136678 ask=1701136678
testing_market_front_touch_sas current=1701136678 ask=1701136678
testing_market_front_desktop_load_sas current=1701136678 ask=1701136678

~~~ Services where current resource id less than need resource id: ~~~

testing_market_front_blue_touch_load_sample_sas current=1309723619 ask=1701136678
testing_market_front_blue_desktop_load_sample_sas current=1309723619 ask=1701136678
testing_market_front_api_load_sample_sas current=1309723619 ask=1701136678
```

Обновить ресурс на сервисах
---------------------------------------------------------------------------

Пример:

```
./marketsre nanny services --filter 'production_market_front.*' update_resource TVM_TOOL_BINARY 2598082190

service production_market_front_vendors_sas contains 901180694 version of TVM_TOOL_BINARY.
service production_market_front_vendors_iva contains 901180694 version of TVM_TOOL_BINARY.
...
Update TVM_TOOL_BINARY in the following services to version 2598082190? [Y/n]: Y
And activate?(It will be restarted if yes) [Y/n]: Y
updating TVM_TOOL_BINARY in production_market_front_vendors_sas
updating TVM_TOOL_BINARY in production_market_front_vendors_iva
...
activating last snapshot in production_market_front_vendors_sas
activating last snapshot in production_market_front_vendors_iva
```


Настройки juggler в nanny
-------------------------
- Вывести кусок из спеки (json), относящийся к настройкам juggler-а
~~~
$ ./marketsre nanny services show_juggler_settings --help
Usage: marketsre nanny services show_juggler_settings [OPTIONS]

  Show settings for juggler in Monitoring Section for nanny services

Options:
  --help  Show this message and exit.
==================================================================
./marketsre nanny services --filter 'testing_market_litmus_client_iva' show_juggler_settings
testing_market_litmus_client_iva
{u'active_checks': [{u'checks': [],
                     u'flap_detector': {},
                     u'module': {u'logic_or': {u'mode': u'CRIT',
                                               u'unreach_mode': u'force_ok'},
                                 u'type': u'logic_or'},
                     u'passive_checks': [{u'juggler_host_name': u'market_runtime',
                                          u'juggler_service_name': u'push-client-auth-check',
                                          u'notifications': [],
                                          u'options': {u'args': [],
                                                       u'env_vars': []}}],
                     u'per_auto_tags': []}],
 u'instance_resolve_type': u'NANNY',
 u'juggler_hosts': [{u'name': u'market_runtime'}],
 u'juggler_tags': [],
 u'namespace': u'market.common'}
~~~

- Добавить в набор джаглерных пассивных проверок проверку авторизации push_client-а.
Если настройки джаглера до этого были выключены, они при этом включатся.
Корректно добавляет, если уже имеются другие проверки.
~~~
$ ./marketsre nanny services set_juggler_settings --help
Usage: marketsre nanny services set_juggler_settings [OPTIONS]

  Set push_client_auth settings check for juggler in Monitoring Section for
  nanny services

Options:
  --help  Show this message and exit.
==================================================================
~~~

- Удалить одну пассивную джаглерную проверку по имени.
Корректно обрадабывает случаи, когда есть несколько проверок и когда она всего одна.
Во втором случае настройки джаглера полностью отключаюжтся.
~~~
$ ./marketsre nanny services remove_juggler_check --help
Usage: marketsre nanny services remove_juggler_check [OPTIONS]
                                                     JUGGLER_SERVICE_NAME
  Remove one passive juggler check by name

Options:
  --help  Show this message and exit.
==================================================================
~~~

- Выключить все джаглерные настройки.
ВНИМАНИЕ: инфа об имеющихся проверках, если они были, будет удалена из спеки!
Чтобы их вернуть, будет не достаточно просто включить джаглерные настройки. Надо будет полностью перенастроить все проверки.
~~~
$ ./marketsre nanny services disable_juggler_settings --help
Usage: marketsre nanny services disable_juggler_settings [OPTIONS]

  Disable all juggler settings

Options:
  --help  Show this message and exit.
==================================================================
~~~




Racktables
===========================================================================
- Вывести информацию о макросе можно следующей командой:
~~~
./marketsre racktables show_macro --help
Usage: marketsre racktables show_macro [OPTIONS]

  Show detailed information about firewall macros.

Options:
  --macro TEXT  macro name  [required]
  --help        Show this message and exit.


==================================================================
./marketsre racktables show_macro --macro _200OKSERVICE_NETS_

{
    "owners": [
        "max-rogov"
    ],
    "owner_service": "",
    "description": "",
    "parent": null,
    "secured": 0,
    "ids": [
        {
            "id": "5421",
            "description": ""
        }
    ],
    "can_create_network": 1,
    "internet": 0,
    "name": "_200OKSERVICE_NETS_"
}
~~~


- Переместить указанный project_id из какой-либо группы в указанную:
~~~
./marketsre racktables move_project_id --help
Usage: marketsre racktables move_project_id [OPTIONS]

  Move project_id from macro it belongs to target_macro

Options:
  --target_macro_name TEXT  target macro name  [required]
  --project_id TEXT         project ID (hex representation) ^0x[0-9a-eA-E]$
                            [required]

  --help                    Show this message and exit.


==================================================================


./marketsre racktables move_project_id --target_macro_name "_STUCK_GENCFG_MARKET_TEST_NETS_" --project_id 0x10b1203
{
    "owners": [
        "dvkhromov",
        "svc_marketito_administration"
    ],
    "owner_service": "",
    "description": "\u041e\u0442\u0441\u0442\u043e\u0439\u043d\u0438\u043a \u0434\u043b\u044f project_id, \u043f\u043e\u0434\u0447\u0438\u0449\u0430\u0435\u043c\u044b\u0445 \u0438\u0437 _GENCFG_MARKET_TEST_NETS_",
    "parent": null,
    "secured": 0,
    "ids": [
.....................
тут очень много всего скрыто, посколку макрос монструозный
.....................
        {
            "id": "10b1203",
            "description": ""
        },
    ],
    "can_create_network": 1,
    "internet": 0,
    "name": "_STUCK_GENCFG_MARKET_TEST_NETS_"
}
Response successfully processed!

~~~
Если project_id уже в целевой группе, api так же скажет, что перемещение прошло успешно.
Тут могут быть проблемы с правами, в макросы gencfg мы ходим от имени робота robot-market-netster
https://yav.yandex-team.ru/secret/sec-01fdwjgkapey8rh1aqjd5vkfv3/explore/versions


- В няне project_id представлены в виде int числа, для удобства добавил конвертер int -> hex
~~~
./marketsre racktables convert_int_to_hex --help
Usage: marketsre racktables convert_int_to_hex [OPTIONS]

  Convert integer to hex value with 0x prefix

Options:
  --value TEXT  Int value for conversion  [required]
  --help        Show this message and exit.
==================================================================
./marketsre racktables convert_int_to_hex --value 100500
0x18894

~~~

Просмотреть потребляемую в YP квоту
==========================================================================

Команда нужно для получения инфорации о сервисе, разнообразной, но пока что возвращает только данные
о потребляемых в YP ресурсах.


```
le087@le087-work:~/devel/work/fuse/arcadia/market/sre/tools/marketsre_cli$ ./marketsre nanny services --filter 'testing_market_clickdaemon_' info
~~~~~~~ Getting info about testing_market_clickdaemon_sas ~~~~~~~~
YP cluster: SAS
ABC quota: abc:service:3285
Count of instances: 2
Used resources:
  CPU, cores: .................. 1.928
  Memory, megabytes: ........... 4096.0
  HDD, megabytes: .............. 260296.0
  HDD IO, megabytes per seconds: 60.0
  SSD, megabytes: .............. 0.0
  SSD IO, megabytes per seconds: 0.0
  IPv4: ........................ 0
  Net, megabytes pers seconds: . 20.0
~~~~~~~ Getting info about testing_market_clickdaemon_iva ~~~~~~~~
Services testing_market_clickdaemon_iva in GENCFG, passed...
~~~~~~~ Getting info about testing_market_clickdaemon_vla ~~~~~~~~
YP cluster: VLA
ABC quota: abc:service:37574
Count of instances: 2
Used resources:
  CPU, cores: .................. 2.0
  Memory, megabytes: ........... 4096.0
  HDD, megabytes: .............. 356352.0
  HDD IO, megabytes per seconds: 32.0
  SSD, megabytes: .............. 0.0
  SSD IO, megabytes per seconds: 0.0
  IPv4: ........................ 0
  Net, megabytes pers seconds: . 0.0
~~~~~~~ Getting info about testing_market_clickdaemon_yp_test_vla ~~~~~~~~
=========================== TOTAL =================================
  CPU, cores: .................. 3.928
  Memory, megabytes: ........... 8192.0
  HDD, megabytes: .............. 616648.0
  HDD IO, megabytes per seconds: 92.0
  SSD, megabytes: .............. 0.0
  SSD IO, megabytes per seconds: 0.0
  IPv4: ........................ 0
  Net, megabytes pers seconds: . 20.0
```



ABC
===

- Запросить роль админа в ABC-группе
(Создавалось под конкретную задачу. Можно легко допилить до запроса произвольной роли.)
~~~
./marketsre abc request_admin_role --help
Usage: marketsre abc request_admin_role [OPTIONS] LOGIN ABC_SERVICE

  Запросить роль администратора для login в abc-группе по slug или id

Options:
  --help  Show this message and exit.
==================================================================
./marketsre abc request_admin_role robot-gencfg-yp-migr 35164
INFO:market.sre.tools.marketsre_cli.commands.abc.abc:Result of role request:
{}
./marketsre abc request_admin_role e-a-sokolov marketito
INFO:market.sre.tools.marketsre_cli.commands.abc.abc:'e-a-sokolov' already has administration role in 'marketito'. Nothing to do for me there.
~~~

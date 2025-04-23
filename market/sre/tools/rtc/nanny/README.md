# Nanny Manager
> A library to manage Nanny services

## Usage example

A easy way to try is using REPL

```
> ya make --checkout market/sre/tools/rtc/repl
> market/sre/tools/rtc/repl/rtc-repl
>>> helpme()
RTC REPL r3249342

It helps you manage Nanny services.

First steps:

>>> import os

>>> manager.list_service_ids(os.getlogin())

>>> service = manager.get_service('testing_market_your_service_sas')

>>> service.id
u'testing_market_your_service_sas'

>>> service.runtime_attrs.instances.extended_gencfg_groups.change_gencfg_release('trunk')

>>> service.runtime_attrs.diff
{update: {u'instances': {update: {u'extended_gencfg_groups': {update: {u'groups': {0: {update: {u'release': u'trunk'}}}}}}}}}

>>> manager.update_service(service)

>>>
```

### Scenarios

The motivation to create the manager was necessity of creating scenarios to configure a number of services.

Some common parts of scenarios
1. Create a service from the template
2. Update Tickets Integration rules
3. Update application resource

An example of creating a new service from the template service
```
>>> from market.sre.tools.rtc.nanny.scenarios.java_service import JavaService

>>> manager = nanny.create_manager(get_token())

>>> template_service = manager.get_service('testing_market_template_service_for_java_iva_copy_d3rp')

>>> application_sandbox_resource_id = 427596416

>>> js = JavaService(manager, template_service.id, application_sandbox_resource_id)

>>> new_service = js.create(service_id='production_test_d3rp_sas', gencfg_group='SAS_MARKET_PROD_D3RP_TEST')

>>> template_service.environment
u'testing'

>>> new_service.environment
u'stable'

>>> pprint(template_service.info_attrs.tickets_integration.service_release_rules[0])
{u'auto_commit_settings': {u'enabled': True,
                           u'scheduling_priority': u'NORMAL'},
 u'desc': u'Application',
 u'filter_params': {u'expression': u'sandbox_release.release_type in ("testing",)'},
 u'queue_id': u'MARKET',
 u'responsibles': [],
 u'sandbox_resource_type': u'MARKET_EMPTY_APP',
 u'sandbox_task_type': u'HTTP_UPLOAD',
 u'ticket_priority': u'NORMAL'}

>>> pprint(new_service.info_attrs.tickets_integration.service_release_rules[0])
{u'auto_commit_settings': {u'enabled': True,
                           u'scheduling_priority': u'NORMAL'},
 u'desc': u'Application',
 u'filter_params': {u'expression': u'sandbox_release.release_type in ("stable",)'},
 u'queue_id': u'MARKET',
 u'responsibles': [],
 u'sandbox_resource_type': u'MARKET_FULFILLMENT_STOCK_STORAGE_APP',
 u'sandbox_task_type': u'HTTP_UPLOAD',
 u'ticket_priority': u'NORMAL'}

>>> nanny.utils.diff(template_service, new_service)
{update: {'runtime_attrs': {update: {u'instance_spec': {update: {u'containers': {3: {update: {u'name': u'stock-storage'}}}}}, u'instances': {update: {u'extended_gencfg_groups': {update: {u'groups': {0: {update: {u'name': u'SAS_MARKET_PROD_D3RP_TEST'}}}}}}}, u'resources': {update: {u'sandbox_files': {0: {update: {u'resource_type': u'MARKET_FULFILLMENT_STOCK_STORAGE_APP', u'task_id': u'187510171', u'resource_id': u'427596416'}}, 2: {update: {u'resource_type': u'MARKET_DATASOURCES_STABLE', u'resource_id': u'413579038'}}}, u'static_files': {0: {update: {u'content': u'{%- set environment = env.BSCONFIG_ITAGS.split("a_ctype_")[1].split()[0] -%}\n{%- set location = env.BSCONFIG_ITAGS.split("a_dc_")[1].split()[0] -%}\n{%- set nginx_log_prefix = "stock-storage" -%}\n{%- set log_files = [\n                        "nginx/" + nginx_log_prefix + "-access-tskv.log",\n                    ]-%}\n{%- set nginx_includes = [\n                            "include/logging",\n                        ]-%}'}}}}}, u'engines': {update: {u'engine_type': u'ISS_SAS'}}}}, 'id': u'production_test_d3rp_sas', 'info_attrs': {update: {u'tickets_integration': {update: {u'service_release_rules': {0: {update: {u'filter_params': {update: {u'expression': u'sandbox_release.release_type in ("stable",)'}}, u'sandbox_resource_type': u'MARKET_FULFILLMENT_STOCK_STORAGE_APP'}}, 1: {update: {u'filter_params': {update: {u'expression': u'sandbox_release.release_type in ("stable",)'}}}}, 2: {update: {u'filter_params': {update: {u'expression': u'sandbox_release.release_type in ("stable",)'}}, u'sandbox_resource_type': u'MARKET_DATASOURCES_STABLE'}}, 3: {update: {u'filter_params': {update: {u'expression': u'sandbox_release.release_type in ("stable",)'}}}}}}}}}}}

>>>
```

## Links

https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/service-repo-api/

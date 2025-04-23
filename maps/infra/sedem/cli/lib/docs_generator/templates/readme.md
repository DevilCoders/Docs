{% if verbose -%}
# {{ namer.human_readable() }}

<< Описание сервиса ?????? >>

{% endif -%}
## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | {{ contacts_string }} |
| Отвественные SRE | {{ sres_string }} |
| Исходники | [{{service.service_path_from_arcadia}}](https://a.yandex-team.ru/arc/trunk/arcadia/{{service.service_path_from_arcadia}}) |
| Сервис в ABC | [{{ namer.abc_service() }}](https://abc.yandex-team.ru/services/{{ namer.abc_service() }}/)|
| Проект в CI | [{{ namer.abc_service() }}](https://a.yandex-team.ru/projects/{{namer.abc_service()}}/ci/actions/launches?dir={{service.service_path_from_arcadia}}) |

{% if service.staging_list(only_activated_stages=False) -%}
## Service infrastructure

{% if service.config('deploy.type') == 'rtc' -%}
### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
{% for staging in service.staging_list(only_activated_stages=False) | sort -%}
| {{ staging.capitalize() }} | [{{ namer.nanny_service(staging=staging) }}](https://nanny.yandex-team.ru/ui/#/services/catalog/{{ namer.nanny_service(staging=staging) }}/) | [ {{namer.yasm_panel_name_readme(staging=staging)}} ](https://yasm.yandex-team.ru/template/panel/{{namer.yasm_panel_name(staging=staging)}}/) | [ {{namer.juggler_host(staging=staging)}} ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D{{namer.juggler_host(staging=staging)}}) |
{% endfor %}
{% elif service.config('deploy.type') == 'garden' -%}
### Instances, monitorings

| Deploy unit | Garden module | Monitoring checks |
| ----------- | ------------- | ----------------- |
{% for staging in service.staging_list() | sort %}{% set environment = staging | replace('testing', 'datatesting') -%}
| {{ staging.capitalize() }} | [{{ environment }} {{ namer.module_name() }}](https://garden.maps.yandex-team.ru/{{ environment }}/{{ namer.module_name() }}/) | [ {{namer.juggler_host(staging=staging)}} ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D{{namer.juggler_host(staging=staging)}}) |
{% endfor %}
{% elif service.config('deploy.type') == 'sandbox' -%}
### Instances, monitorings

| Deploy unit | Sandbox object | Monitoring checks |
| ----------- | -------------- | ----------------- |
{% for deploy_unit in service.resources.sandbox_deploy_units() -%}
{% if deploy_unit.unit_type == 'scheduler' -%}
| {{ deploy_unit.name }} | [ {{namer.sandbox_scheduler_name(deploy_unit=deploy_unit.name)}} ](https://sandbox.yandex-team.ru/schedulers/?all_tags=true&tags=SEDEM_MANAGED,SERVICE:{{ namer.sandbox_scheduler_name(deploy_unit=deploy_unit.name) }}) | [ {{namer.juggler_host(staging=deploy_unit.name)}} ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D{{namer.juggler_host(staging=deploy_unit.name)}}) |
{% else -%}
| {{ deploy_unit.name }} | [ {{namer.sandbox_template_alias(deploy_unit=deploy_unit.name)}} ](https://sandbox.yandex-team.ru/template/{{ namer.sandbox_template_alias(deploy_unit=deploy_unit.name) }}) | [ {{namer.juggler_host(staging=deploy_unit.name)}} ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D{{namer.juggler_host(staging=deploy_unit.name)}}) |
{% endif -%}
{% endfor %}
{% endif -%}
[Monitorings all (tag={{namer.juggler_prj()}})](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3D{{namer.juggler_prj()}})

{% if balancers_setup -%}
### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
{% for staging, balancers_def in balancers_setup.items() | sort -%}
{% for balancer_name, balancer_def in balancers_def.items() | sort -%}
| {{ staging.capitalize() }} | {{ balancer_name }} | {{ balancer_def.awacs }} | {{ balancer_def.panel }} | {{ balancer_def.nanny }} |
{% endfor -%}
{% endfor %}
{% endif -%}

{% if l3_only_balancers_setup -%}
### L3-only balancers

| Staging | Name | FQDN                    |
| ------- | ---- |-------------------------|
{% for staging, balancers_def in l3_only_balancers_setup.items() | sort -%}
{% for balancer_name, balancer_def in balancers_def.items() | sort -%}
| {{ staging.capitalize() }} | {{ balancer_name }} | {{ balancer_def.fqdn }} |
{% endfor -%}
{% endfor %}
{% endif -%}

{% if service.config('deploy.type') == 'rtc' -%}
### Firewall macroses

| staging | URL |
|---|---|
{% for staging in service.staging_list(only_activated_stages=False) | reject("==", "prestable") | sort -%}
| {{ staging.capitalize() }} | [ \{{ namer.network_macro_name(staging=staging) }} ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name={{ namer.network_macro_name(staging=staging) }} ) |
{% endfor %}
{% endif -%}
{% endif -%}
{% if verbose -%}
## What happens when service is down

TODO: Напишите, что происходит при отказе сервиса

{% if service.staging_list(only_activated_stages=False) and service.config('deploy.type') == 'rtc' -%}
## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE ''<<yacare-service-name>>'.maps.yandex.net' limit 1; |

{% endif -%}
## How to fix common problems

{% if service.config('deploy.type') == 'rtc' -%}
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

{% endif -%}
TODO: Добавьте описание, как чинить ваш сервис

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)

## Known clients

TODO: Сюда напишите список известных клиентов

{% endif -%}
{% if service.config('dependencies.datasets', default=False) -%}
## Ecstatic Datasets

| Stable | Testing |
| ------ | ------- |
{% for dataset in service.config('dependencies.datasets') -%}
| [{{ dataset }}](http://ecstatic.maps.yandex.net/pkg/{{ dataset }}/versions) | [{{ dataset }}](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/{{ dataset }}/versions) |
{% endfor %}
{% endif -%}
{% if verbose -%}
{% if service.staging_list(only_activated_stages=False) and service.config('deploy.type') == 'rtc' -%}
## Persistent Volumes

* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)

{% endif -%}
{% endif -%}
{% if service.config('deploy.type') == 'rtc' -%}

## Regression tests

{% if load_tests -%}
| Имя теста | Тикет | Запустить нагрузочный тест | Lunapark |
| --------- | ----- | -------------------------- | -------- |
{% for load_test in load_tests -%}
| {{load_test.test_name}} | {{load_test.st_ticket_link}} | {% if verbose %}Кнопка запуска — [на странице SEDEM_SERVICE_PAGE](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22{{namer.canonical()}}%22%7D). Или следуйте инструкциям ниже.{% else %}{{load_test.launch_button}}{% endif %} | {{load_test.lunapark_link}} —> `{{load_test.slug}}` |
{% endfor -%}
{% else -%}
Нагрузочные тесты через sedem не сконфигурированы. [Создать нагрузочные тесты](https://docs.yandex-team.ru/sedem/services/nanny#load-testing).
{% endif %}
Sandbox-шедулер: [Общий шедулер регрессионных нагрузочных тестов](https://sandbox.yandex-team.ru/scheduler/702021)

Провести нагрузочный тест вручную:

+ воспользуйтесь кнопкой `Запустить` на [странице сервиса в SEDEM_SERVICE_PAGE в Sandbox](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs=%7B%22sedem_service%22:%20%22{{namer.canonical()}}%22%7D).
+ или возьмите [шаблон](https://sandbox.yandex-team.ru/template/MAPS_CORE_COMMON_LOAD_TESTING_TEMPLATE/view) —> нажмите `Create new task` —> наберите имя sedem-сервиса, уберите галочку «Run for all tests in service», наберите имя теста.
{% endif -%}

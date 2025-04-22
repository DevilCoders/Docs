# infra-cfg-juggler
Config templates for Juggler monitoring (https://wiki.yandex-team.ru/SM/Juggler/).
Configs are generated and pushed to Juggler every 10 minutes by [cron-task](https://tariff-editor.taxi.yandex-team.ru/dev/cron/clowny_alert_manager-crontasks-juggler_alert_generator)

## ЕСЛИ ВАМ НУЖНО ТОЛЬКО ДОБАВИТЬ/ИЗМЕНИТЬ ПОЛУЧАТЕЛЕЙ АЛЕРТОВ В ТЕЛЕГРАМ ДЛЯ СЕРВИСА

Это можно сделать через админку, см. https://wiki.yandex-team.ru/taxi/backend/hejmdal/alert-manager/unified-recipients/

## scripts
#### add_template.py
This script is useful when you need to add a template to multiple check-files.
The following example adds template 'hejmdal-rtc-resource-usage' to all stable rtc checks:
`$ infra-cfg-juggler: python3 scripts/add_template.py --dir 'checks' --template 'hejmdal-rtc-resource-usage' --mask 'rtc_.*_stable'`

#### api-proxy/generate.py
This scripts generates solomon alerts and juggler checks settings for api-proxy handlers. Each handler's alerts and checks are stored in a separate file, where there is a service for each of the handler's resources. It is possible to configure thresholds per resource and/or change the list of resources via `settings.yaml` config file.

Note: this scripts requires `jinja2` and `pyyaml` packages.

## Run tests

`make test`

## Automerge

За пулл-реквестами в `infra-cfg-juggler` следит робот. Если ваш пулл-реквест соответствует некоторым критериям, то робот его окнет, и вы сможете замержиться без привлечения группы Диагностики к ревью. **Робот пишет в пулл-реквест дальнейшие инструкции после загрузки каждого диффсета**. Обращаться в [чат поддержки](https://nda.ya.ru/t/ePhVLReX4jWesx) нужно, только если об этом написал робот или его нет 15 минут.

Вкратце, критерии нацелены на то, чтобы вы не могли отредактировать алерты, которые рискуют разбудить не вас. Критерии подробно:
1) В пулл-реквесте не должно быть файлов вне `/taxi/infra/infra-cfg-juggler`
2) Файлы в папке `/taxi/infra/infra-cfg-juggler/solomon_alerts` может редактировать кто угодно без ограничений
3) Файлы внутри `/taxi/infra/infra-cfg-juggler/checks` с префиксами `rtc_` могут редактировать ответственные за сервис (т.е либо создатель пулл-реквеста, либо аппрувер должен быть в пересечении ответственных по всем сервисам из пулл-реквеста). Ответственные сервиса -- дежурная группа + мейнтейнеры. Если у сервиса нет круглосуточной дежурной группы, считаем что у сервиса нет ответственных.
4) Пулл-реквест окнул хотя бы 1 живой человек (какой именно, робот уточнит в комментариях)

Во всех остальных случаях требуется ревью группы Диганостики.

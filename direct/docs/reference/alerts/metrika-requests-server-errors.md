# metrika_requests_server_errors

[Алерт в juggler](https://juggler.yandex-team.ru/check_details/?host=direct.disaster_alerts&service=metrika_requests_server_errors)
[Алерт в Solomon](https://solomon.yandex-team.ru/admin/projects/direct/alerts/metrica_requests_server_errors_disaster)
[исходник](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/integrations/metrika.py)

## Описание { #description }
Алерт на количество серверных ошибок (5xx, подключения, таймутов) при запросах в Метрику.
Пока отслеживаются только запросы из perl.


## Диагностика { #diagnostics }
Посмотреть [графики](https://solomon.yandex-team.ru/?b=6h&cluster=app_java-intapi&cs=default&env=production&external_system=metrika&graph=auto&host=CLUSTER&method=*&project=direct&sensor=reqs.count&service=external-metrics&stack=false&l.interpreted_status=*) — их можно отфильтровать
по конкретной ручке и по статусу (метки `method` и `interpreted_status`).
Значения — это число запросов за 15 секунд.

Также можно попробовать поискать по messages логу сообщения об ошибках, содержащие имя ручки или адрес метрики (audience-intapid.metrika.yandex.ru, internalapi.metrika.yandex.ru).

## Решение { #solution }
Сообщить о проблеме дежурному [Metrika API Support+Monitoring](https://duty.mtrs.yandex-team.ru/project/metrika/duty_group_dashboard/api/):
- с какой ручкой проблемы
- как много
- когда начались

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [Графики запросов](https://solomon.yandex-team.ru/?b=6h&cluster=app_java-intapi&cs=default&env=production&external_system=metrika&graph=auto&host=CLUSTER&method=*&project=direct&sensor=reqs.count&service=external-metrics&stack=false&l.interpreted_status=*)

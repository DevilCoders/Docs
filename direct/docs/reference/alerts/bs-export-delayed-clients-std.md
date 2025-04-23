# queue_std.delayed_clients_count

[juggler](https://juggler.yandex-team.ru/check_details/?host=direct.perl_bsexport&service=queue_std.delayed_clients_count&query=&last=1DAY)

## Описание { #description }
Этот алерт зажигается при наличии в std-очереди кампаний, стоящих там более 90 минут.
Статус алерта зависит от количества клиентов с такими кампаниями:
- OK — нет ни одного клиента или он только один
- WARN — два и более клиентов
- CRIT — больше 20 клиентов

Если клиентов много — это можно говорить о:
- у нас массовый баг или ошибки на стороне БК
- какая-то конкретная кампания сломалась и к ней "прилипают" (становятся залоченными на итерацию) нормальные кампании и не отправляются из-за этого 

По алерту есть звонок и старт протокола (SPI).

## Диагностика { #diagnostics }
По дашборду об [очереди STD](https://solomon.yandex-team.ru/?project=direct&dashboard=bs-export-queue-templated&queue=std&service=bs-export-queue&cluster=app_java-jobs)
и [общему дашборду](https://solomon.yandex-team.ru/?project=direct&dashboard=bs-export-perl&b=6h) экспорта.

## Решение { #solution }
Исследовать на конкретных примерах кампаний по [общей инструкцию по диагностике экспорта](../bs-export-diag.md#how-to) почему кампании не отправляются и устранять их.

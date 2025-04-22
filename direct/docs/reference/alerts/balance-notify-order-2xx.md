# balance-notifyOrder-2xx

[Алерт в solomon](https://solomon.yandex-team.ru/admin/projects/direct/alerts/balance-notifyOrder-2xx)

## Описание { #description }

Алерт на количество успешных нотификаций за промежуток времени. Срабатывает при падении значений ниже определенного числа (выведенного из опыта).
Это может иметь три причины (что делать — ниже):
- что-то сломалось у нас — нотификации не доходят, доходят но не обрабатываются корректно
- что-то сломалось в балансе
- "новый год" (снижение деловой активности)

{% note alert "Для нас эти нотификации очень важны" %}

Полученные из них актуальные суммы на кампаниях мы отправляем в БК (чтобы продолжались показы рекламы),
по ним мы показываем остатки в интерфейсе и пишем уведомления.
В случае перерыва в приеме нотификаций более чем на два часа — начинаются остановки кампаний в БК из-за окончания денег.

{% endnote %}

## Диагностика { #diagnostics }
### что-то сломалось у нас { #our-problem }
1. проверить исправность приборов: 
   1. зайти по ssh на сами машинки интапи
   1. посмотреть и погрепать nginx-access логи на предмет наших нотификаций.
   1. Если они там есть и их много, а алерт горит — искать что сломалось в мониторинге и чинить его
1. если нотификации к нам приходят, но не обрабатываются успешно — разбираться по плану из [{#T}](balance-notify-order-5xx.md)
1. если никаких признаков нотификаций нет, то действуем по [следующему плану](#balance-problem)

### что-то сломалось у баланса { #balance-problem }
1. Проверить рассылки `back-office@` , `sales-launch@` на наличие писем вида "Проблемы в работе системы Баланс".
Если у баланса известная проблема с тем, что прилег Oracle — не нужно их лишний раз беспокоить, починку это не ускорит
1. если информации о проблемах не обнаружилось, то ищем [дежурного у Баланса](../duty.md#balance). На чатики не полагаемся, звоним телефоном (рабочим, мобильным). Если дозвониться не получается — звоним его руководителю или дежурному админу эксплуатации платежных систем.
1. Представляемся ("я из Директа"), описываем проблему ("у нас пропали от вас нотификации о зачислении средств"), интересуемся "известная ли эта проблема, есть ли сроки починки, тикет для отслеживания, правильный контакт для уточнения статуса и можем ли помочь какой-то информацией".
1. Дальше по ситуации

### "новый год"
В канун нового года, примерно с 31 декабря по 1-2 января,
активность и число приносимых нам (Директу, Яндексу) денег (и нотификаций о них) снижаетя настолько, что пробивает порог алерта.
В такой ситуации нужно убедиться, что нотификации не пропали совсем (можно по графику).
Если какое-то количество нотификаций осталось — на ближайшие 2—4 часа считаем ситуацию "ОК". Если нет, действуем по плану будто [сломалось у нас](#our-problem)

## Подробности { #details }
**Нотификация** — это POST-вызов Балансом нашей json-ручки `intapi.direct.yandex.ru/BalanceClient/NotifyOrder` для изменения в нашей базе суммы зачисленного на заказе.

Со стороны баланса это работает так: у них есть очередь (где-то в БД) и сервис "нотификатор",
который в бесконечном цикле берет нотификации из очереди и отправялет к нам по одной.
При ошибке отправки — нотификация перекладывается в конец очереди
(и не удаляется, мы "любимый" сервис для которого так _нужно__) и будет повторена позднее.

С нашей стороны обработкой нотификаций занимается [контроллер](https://a.yandex-team.ru/arc/trunk/arcadia/direct/intapi/src/main/java/ru/yandex/direct/intapi/entity/balanceclient/controller/BalanceClientController.java?#L138) в java-INTAPI.

Все логи в логвьювере:
- запросы — в логе `ppclog_cmd`, `cmd`=`BalanceClient`. [готовая ссылка](https://direct.yandex.ru/logviewer/#~(logType~'ppclog_cmd~form~(fields~(~'log_time~'uid~'role~'cluid~'cid~'service~'cmd~'runtime~'param~'http_status~'response~'ip~'reqid~'tvm_service_id~'tvm_service_name)~conditions~(cmd~'BalanceClient.NotifyOrder2~service~'direct.java.intapi)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- ошибки/прочее в логе `messages`, `service`=`direct.intapi`, `method`=`BalanceClient.NotifyOrder2`. [готовая ссылка](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'BalanceClient.NotifyOrder2~service~'direct.intapi)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer запросы](https://direct.yandex.ru/logviewer/#~(logType~'ppclog_cmd~form~(fields~(~'log_time~'uid~'role~'cluid~'cid~'service~'cmd~'runtime~'param~'http_status~'response~'ip~'reqid~'tvm_service_id~'tvm_service_name)~conditions~(cmd~'BalanceClient.NotifyOrder2~service~'direct.java.intapi)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Logviewer ошибки/messages](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'BalanceClient.NotifyOrder2~service~'direct.intapi)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [График (не за интервал, просто RPS)](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-intapi&service=java-monitoring&l.controller=BalanceClientController&l.method=notifyOrder&l.env=production&l.status=2xx&l.host=CLUSTER&l.sensor=reqs.count&graph=auto&transform=differentiate&downsampling=off&b=1d&e=&max=5) из саммих веб-серверов
- [График числа нотификаций за интервал](https://ppcgraphite.yandex.ru/grafana/dashboard/db/direct-group-internal-systems-tv?refresh=1m&orgId=1&panelId=19&fullscreen) по логам обрабатанных нотификаций из кликхауса
- [код контроллера](https://a.yandex-team.ru/arc/trunk/arcadia/direct/intapi/src/main/java/ru/yandex/direct/intapi/entity/balanceclient/controller/BalanceClientController.java?#L138)
- [График 500к](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-intapi&service=java-monitoring&l.controller=BalanceClientController&l.method=notifyOrder&l.env=production&l.status=5xx&l.host=CLUSTER&l.sensor=reqs.count&graph=auto&downsampling=off&transform=differentiate&b=1d&e=)

## PromoactionModerationEventsProcessor

### Продукт/подсистема

Модерация самостоятельного библиотечного объекта "Промоакция".


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию промоакции.


### Датафлоу

Классический модерационный ESS процессор. Хотя акция привязывается к баннеру, модерируется она самостоятельно без учёта привязки к конкретному объявлению.

- Отслеживает события в таблице [ppc.promoactions](https://direct-dev.yandex-team.ru/db/ppc/tables/promoactions.html).
- Отправляет ресурс в Модерацию через LogBroker, используя топик [ess--promoaction-moderation](https://lb.yandex-team.ru/lbkx/accounts/direct/ess/promoaction-moderation)


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.PromoactionModerationEventsProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'promoaction.PromoactionModerationEventsProcessor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Логи объектов изменений](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(conditions~(topic~'*25ess--promoaction-moderation)~fields~(~'binlog_time~'topic~'source~'seqNo~'logic_object_attr~'logic_object_value~'logic_object~'gtid~'reqid)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Логи ess_moderation](https://direct.yandex.ru/logviewer/#~(logType~'ess_moderation~form~(conditions~(data~'*25*22type*22*3a*22promo_extension*22*25)~fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Промоакции не будут отправляться в Модерацию.


### Как пользователи (или команда) заметят проблему и через какое время

По статусу на гриде промоакций (в новом интерфейсе можно зайти через выпадающий список "Библиотека" или по [прямой ссылке](https://direct.yandex.ru/dna/library/promoExtensions)) долго находится в Модерации.

Баннеры будут показываться без промоакций.


### Контакты разработчиков и менеджеров

Менеджеры: [Александр Липчин](https://staff.yandex-team.ru/lipchin)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.

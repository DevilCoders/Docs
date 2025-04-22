## BsExportFeedsProcessor

### Продукт/подсистема

ESS-транспорт в БК/CaeSaR.


### Роль в работе продукта/подсистемы

Получает события, что в БД изменилась информация о фидах и экспортирует информацию об этих изменениях в БК.


### Датафлоу

Классический ESS-процессор для транспорта в БК (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения фидов в MySQL (они приходят в ESS-процессор из ESS-роутера через `LogBroker`).
- По полученным событиям достает из MySQL актуальные данные.
- Отправляет обновленные данные в реплицируемую таблицу* [markov.//home/adv/DirectFeeds](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/adv/DirectFeeds) и [markov.//home/adv/vault/DirectFeedsAccess](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/adv/vault/DirectFeedsAccess). Вторая содержит пароли к фидам и имеет ограниченный доступ.

* Актуальные пути к таблицам формируется на основе полей `dynamic-yt/tables/bs-export/feeds` и `.../feeds-access` в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf).

### Способы наблюдения за текущим состоянием

- [ESS-дашборд](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production)
- [Дашборд по ESS-транспорту](https://solomon.yandex-team.ru/?project=direct&dashboard=new-bs-transport)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fexport-bs-feeds&b=2021-03-21T14%3A18%3A10.000Z&e=2021-03-22T14%3A18%3A10.000Z)
- [Логи событий изменения](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--export-bs-feeds)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи экспорта](https://direct.yandex.ru/logviewer#~(logType~'bsexport_data~form~(fields~(~'log_time~'data_type~'cid~'pid~'bid~'data)~conditions~(data_type~'feed)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи процессора](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'feeds.BsExportFeedsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportFeedsProcessor.working.production&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы

Отправка фидов новым транспортом в БК. На текущий момент (2021-03-22) потребителей таблиц нет, функциональность некритичная, но при отставании в вычитывании промежуточного топика загорится мониторинг у команды LogBroker.


### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

Неделя.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)
- [Отключение правила через пропертю disabled_ess_rules](https://direct.yandex.ru/internal_tools/#set_typed_ppc_property). Если на момент поломки у таблицы все еще нет потребителей, можно добавить в пропертю значение `export_bs_feeds`.


### Известные причины поломок

- Проблемы с LogBroker.
- Работы на YT кластере Markov.
- Не работает весь ESS-контур.


### Дополнительно: тонкости и подводные камни

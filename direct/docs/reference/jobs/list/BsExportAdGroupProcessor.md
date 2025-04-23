## BsExportAdGroupProcessor

### Продукт/подсистема

ESS транспорт в БК/CaeSaR.


### Роль в работе продукта/подсистемы

Транспорт групп в БК/CaeSaR. Получает события, что в БД изменилась информация о группе и экспортирует информацию об этих изменениях в БК.


### Датафлоу

Классический ESS-процессор для транспорта в БК (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения группах объявлений в MySQL (`phrases`, `adgroups_internal`...) (они приходят в ESS-процессор из ESS-роутера через `LogBroker`).
- По полученным событиям достает из MySQL актуальные данные.
- Сохраняет новые данные в YT в реплицируемую таблицу [markov.//home/adv/DirectAdGroups](https://yt.yandex-team.ru/markov/navigation?path=//home/adv/DirectAdGroups).


### Способы наблюдения за текущим состоянием

- [Общий дашборд ESS](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production&b=2021-03-14T09%3A41%3A19.102Z&e=2021-03-15T09%3A41%3A19.102Z)
- [Дашборд по ESS-транспорту](https://solomon.yandex-team.ru/?project=direct&dashboard=new-bs-transport)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fexport-bs-ad-groups&b=1d&e=)
- [Логи событий изменения](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--export-bs-ad-groups)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи экспорта](https://direct.yandex.ru/logviewer#~(logType~'bsexport_data~form~(fields~(~'log_time~'data_type~'cid~'pid~'bid~'data)~conditions~(data_type~'ad_group)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportAdGroupProcessor.working.production&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы




### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

Как можно раньше.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

- Проблемы с LogBroker.
- Работы на YT кластере Markov.
- Не работает весь ESS-контур.


### Дополнительно: тонкости и подводные камни

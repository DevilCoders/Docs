## BsExportAdGroupShowConditionProcessor

### Продукт/подсистема

ESS-транспорт в БК/CaeSaR.


### Роль в работе продукта/подсистемы

ESS транспорт в БК/CaeSaR информации об условиях показа на группе в БК/CaeSaR.


### Датафлоу

Классический ESS-процессор для транспорта в БК (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения таргетингов на группах объявлений (гео, тип устройства для РМП и т.п.)
- По полученным событиям достает из MySQL актуальные данные.
- Сохраняет новые данные в YT в реплицируемую таблицу [markov.//home/adv/DirectAdGroupShowConditions](https://yt.yandex-team.ru/markov/navigation?path=//home/adv/DirectAdGroupShowConditions).
- Добавляет данные в YT в очередь для CaeSaR [markov.//home/adv/queues/DirectAdGroupShowConditionsQueue](https://yt.yandex-team.ru/markov/navigation?path=//home/adv/queues/DirectAdGroupShowConditionsQueue).

### Способы наблюдения за текущим состоянием

- [Общий дашборд ESS](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production&b=1d&e=)
- [Дашборд по ESS-транспорту](https://solomon.yandex-team.ru/?project=direct&dashboard=new-bs-transport)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fexport-bs-ad-group-show-conditions&b=1d&e=)
- [Логи событий изменения](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--export-bs-ad-group-show-conditions)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи экспорта](https://direct.yandex.ru/logviewer#~(logType~'bsexport_data~form~(fields~(~'log_time~'data_type~'cid~'pid~'bid~'data)~conditions~(data_type~'ad_group_show_condition)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportAdGroupShowConditionProcessor.working.production&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы

Отправка таргетингов новым транспортом в БК. Баннеры либо не будут крутиться, либо будут крутиться с устаревшими таргетингами - это критично.


### Как пользователи (или команда) заметят проблему и через какое время

- Пользователи могут увидеть по статистике, что баннеры откручивались не по тем таргетингам, которые они указали.


### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Николай Кондрашов](https://staff.yandex-team.ru/nikondr)


### Желательное время исправления в случае поломки

Максимально оперативно.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

- Проблемы с LogBroker.
- Работы на YT кластере Markov.
- Не работает весь ESS-контур.


### Дополнительно: тонкости и подводные камни

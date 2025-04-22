## MetrikaBannerUpdateProcessor

### Продукт/подсистема

Интеграция с Метрикой.


### Роль в работе продукта/подсистемы

Транспорт информации о баннерах в Метрику. Получает события, что в БД изменилась информация о баннерах и экспортирует информацию об этих изменениях через LogBroker в Метрику.


### Датафлоу

ESS-процессор для транспорта в Метрику (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения в баннерах в MySQL (они приходят в ESS-процессор из ESS-роутера через `LogBroker`).
- По полученным событиям достает из MySQL актуальные данные.
- Записывает их в LogBroker в топик [direct/export/metrika/banner-update](https://logbroker.yandex-team.ru/lbkx/accounts/direct/export/metrika/banner-update?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1616347263246&metricsTo=1616433663247&sortOrder=%22default%22).


### Способы наблюдения за текущим состоянием

- [ESS-дашборд](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fmetrika-banner-update&b=2021-03-21T14%3A18%3A10.000Z&e=2021-03-22T14%3A18%3A10.000Z)
- [График количества отправленных в Метрику объектов по шардам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.env=production&l.sensor=written_metrika_objects&graph=auto&stack=false&transform=differentiate&b=2021-03-21T17%3A24%3A42.687Z&e=2021-03-22T17%3A24%3A42.687Z)
- [Логи процессора](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'bannerupdate.MetrikaBannerUpdateProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MetrikaBannerUpdateProcessor.working.production&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы

На текущий момент (2021-03-22) Метрика так и не перешла на использование топика, так что никакая функциональность не пострадает. Если будет отставание в вычитывании промежуточного топика ESS, то это зажжет алерты у команды LogBroker.


### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

[Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

Неделя.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)
- [Отключение правила через пропертю disabled_ess_rules](https://direct.yandex.ru/internal_tools/#set_typed_ppc_property). Если на момент поломки у топика все еще нет потребителей, можно добавить в пропертю значение `metrika_banner_update`.


### Известные причины поломок

- Проблемы с LogBroker.
- Работы на YT кластере Markov.
- Не работает весь ESS-контур.


### Дополнительно: тонкости и подводные камни

# AbDataPrepareJob

## Описание

### Продукт/подсистема

АБ-тестирование продуктов/фичей Директа.


### Роль в работе продукта/подсистемы

Джоба готовит подневные данные в YT для расчета АБ-метрик в [Cofe](https://wiki.yandex-team.ru/serp/experiments/cofe/doc/).


### Датафлоу

Джоба параметризованная. <br/>
Каждому параметру соответствует комбинация одного YQL-скрипта и одного из двух кластеров (`Hahn`/`Arnold`). <br/>
Каждый YQL-скрипт сохраняет результаты в новую подневную таблицу. <br/>
YQL-скрипты лежат в [ресурсах приложения jobs](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/abt).

Для каждого параметра джобы:
- Читает из ppc-property дату последнего успешного расчета, далее делает расчет со следующей даты.
- С помощью YQL читает данные (из таблиц Директа и БК, но технических ограничений нет) и сохраняет результат для соответствующего дня в директории [//home/direct/logs/ab_prepared_data](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/ab_prepared_data).

Каждый запрос в нормальной ситуации отрабатывает один раз в день по готовности всех таблиц, нужных для запроса. Если по какой-то причине не удается сделать расчет вовремя, то при устранении неполадок джоба нагонит график (пропусков не будет).


### Способы наблюдения за текущим состоянием

- Ppc-property вида `last_ab_prepared_data_PARAM_<CLUSTER>---<file>.sql` содержат дату последнего расчета для каждой пары "параметр джобы - кластер" (например, `last_ab_prepared_data_PARAM_HAHN---prepare_uaas_log.sql`).
- [Juggler-проверка](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Djobs.AbDataPrepareJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'abt.AbDataPrepareJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Пострадает расчет метрик для АБ-экспериментов за некоторые даты. После починки данные за эти дни будут пересчитаны. Влияет только на каманду директа, критичность средняя&


### Как пользователи (или команда) заметят проблему и через какое время

Команда директа может заметить отсутствующие метрики за конкретные даты в абшнице.


### Контакты разработчиков и менеджеров

Разработчики: [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

День - два.


### Способы регулирования работы джобы



### Известные причины поломок

Отставание таблиц БК.


### Дополнительно: тонкости и подводные камни

Все запросы конфигурируются классами в [коде](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/abt/queryconf). В конфиге описано, какие условия должны быть выполнены, чтобы запрос отработал за конкретную дату.

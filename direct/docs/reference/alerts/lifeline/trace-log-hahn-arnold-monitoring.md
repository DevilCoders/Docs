# Алерты наличия вызовов yql запросов на хане или арнольде lifeline_traceLogYqlExecute

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogYqlExecute-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogYqlExecute-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogYqlExecute-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogYqlExecute-direct.web.perl)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogYqlExecute-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogYqlExecute-direct.web.java)

## Описание { #description }

Алерты появления запросов в хан или арнольд.
Строится на основе трейс логов. Срабатывает при появлении хотя бы одного такого запроса.
Остается гореть в течение 24 часов после срабатывания.

Появление такого запроса является проблемой. В данные кластера нельзя ходить из real-time ручек, т.к. они не дают никаких гарантий на время ответа.
Если такие запросы появились с релизом в существующих ручках, то стоит задуматься об откате задачи. Если это новая функциональность, то переделать ее.


## Диагностика { #diagnostics }

### Проверить, не выкладывался ли недавно релиз
1. В описании каждой алерта в juggler есть ссылка, перед которой написано **AppVersionUrl**, на график с изменением версий. [Пример алерта](https://juggler.yandex-team.ru/raw_events/?query=host%3Dlifeline_traceLogCpu-direct.web.grid%26service%3Dgrid.addAds)
   Также в описании алерта есть ссылка на график. Перед ссылкой написано **Url:**
   Сравнить два графика с выкладной релиза и проблемой в алерте.
3. Попробовать найти среди тикетов релиза те, которые могли задеть. Если проблема найдена, то завести тикет на разработчика.
4. Если изменение ожидаемо, то добавить ручку в исключения. [Пример конфига](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/has_problem/traceLogYqlExecute-direct.web.grid.api.json) по сервису, куда добавлять исключения
5. Если тикет не найдет, то завести задачу на разбор в zbp.

### Другое
Если релиз не выкладывался, то возможно это редкие запросы. Завести тикет в zbp с тем, чтобы убрать такие запросы. На время починки добавить исключения в [конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/has_problem/traceLogYqlExecute-direct.web.grid.api.json).

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer тейсов с запросами в hahn/arnold](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(from~'20210419T000000~to~'20210419T235959~fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'*25TraceLogSystemMonitoringJob*25~message~'*25traceLogYqlExecuteMonitoringDataProcessor*25)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Пример конфигурации алерта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/has_problem/traceLogYqlExecute-direct.web.grid.api.json)

# Алерты наличия многошардового запроса lifeline_traceLogMultiShard

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMultiShard-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMultiShard-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMultiShard-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMultiShard-direct.web.perl)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMultiShard-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMultiShard-direct.web.java)

## Описание { #description }

Алерты на появления запросов в большое количество шардов (>6).
Строится на основе трейс логов. Срабатывает при появлении хотя бы одного многошардового запроса.
Остается гореть в течение 24 часов после срабатывания.

## Диагностика { #diagnostics }
### Проверить, не выкладывался ли недавно релиз { #new-multishard }
1. В описании каждой алерта в juggler есть ссылка, перед которой написано **AppVersionUrl**, на график с изменением версий. [Пример алерта](https://juggler.yandex-team.ru/raw_events/?query=host%3Dlifeline_traceLogCpu-direct.web.grid%26service%3Dgrid.addAds)
   Также в описании алерта есть ссылка на график. Перед ссылкой написано **Url:**
   Сравнить два графика с выкладной релиза и проблемой в алерте.
3. Попробовать найти среди тикетов релиза те, которые могли задеть. Если проблема найдена, то завести тикет на разработчика.
4. Если изменение необходимо, то в тикете ручка добавить в исключения. Пример конфига, в который нужно добавить исключение, в полезных ссылках.
5. Если нет, то заменить многошардовый запрос на другой.

### Другое
Возможно, запрос выполняется редко и просто не был добавлен в исключения раньше. Нужно добавить его в исключения в конфиге.

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer мультишардовых запросов](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'*25TraceLogSystemMonitoringJob*25~message~'*25for_data_row*25method*3dads.update*25)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [LogViewer количества вызовов ручки](https://direct.yandex.ru/logviewer/#~(logType~'trace~form~(fields~(~'log_time)~conditions~(method~'keywordbids.get)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false~showStats~true~sortByCount~false~logTimeGroupBy~'HOUR))$)
- [Пример конфигурации алерта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/has_problem/traceLogMultiShard-direct.web.grid.api.json)

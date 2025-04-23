# Алерты времени выполнения rest части запросов lifeline_traceLogTimeSpentRest

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpentRest-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpentRest-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpentRest-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpentRest-direct.web.perl)

[Алерт в solomon для graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpentRest-direct.web.grid.api)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpentRest-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpentRest-direct.web.java)

## Описание { #description }

Алерты на время выполнения rest части запросов. Строится на основе трейс логов. Срабатывает при превышении перцентиля, описанного в [конфиге сервиса](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogDbWriteCalls-direct.intapi.json?rev=r8120867#L6), перцентиля заданного порога.
Остается гореть в течение трех-четырех часов после срабатывания.

## Диагностика { #diagnostics }
{% include [links](_includes/release-threshold.md) %}
### Другое
1. Еще одной возможной причиной пробития порога могут быть большие клиенты, которые сделали много запросов с большим количеством данных. Задаутаймить проверку, поменять пороги или добавить трейсинга, чтобы уменьшить rest часть запроса.

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer всех трейс логов ручки](https://direct.yandex.ru/logviewer/#~(logType~'trace~form~(fields~(~'log_time~'service~'method~'tags~'trace_id~'span_id~'ela~'cpu_user~'profile)~conditions~(method~'keywordbids.get)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [График с перцентилем](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=common-metrics&l.host=CLUSTER&l.sensor=traceLogTimeSpentRest&l.monitoring_method=grid.api.BannersQuery&graph=auto&transform=moving_average&movingWindow=1h&overLinesTransform=WEIGHTED_PERCENTILE&percentiles=95&b=1w&e=&l.bin=*)
- [Пример конфигурации алерта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogTimeSpentRest-direct.web.grid.json)

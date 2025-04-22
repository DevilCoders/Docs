# Алерты потребления cpu lifeline_traceLogCpu

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogCpu-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogCpu-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogCpu-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogCpu-direct.web.perl)

[Алерт в solomon для graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogCpu-direct.web.grid.api)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogCpu-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogCpu-direct.web.java)

## Описание { #description }

Алерты на потребление cpu. Строится на основе трейс логов. Срабатывает при превышении перцентиля, описанного в [конфиге сервиса](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogDbWriteCalls-direct.intapi.json?rev=r8120867#L6), заданного порога.
Остается гореть в течениие трех-четырех часов после срабатывания.

Превышение порога может иметь следующие причины (что делать — ниже):
- проблемы на стороне Директа
- флапы

## Диагностика { #diagnostics }
{% include [links](_includes/release-threshold.md) %}

### флапы { #flap }
1. еще одна возможная причина пробития порога - пришел большой клиент и сделал много запросов с большим количеством данных. Задаутаймить проверку или поменять пороги.
1. Если порог пробит долгое время и нет кандидата на источник, то проверить по [инструкции](../../../incidents/how-to-report.md) можно ли считать проблему аварией, если нет, то завести задачу в zbp. Повысить порог на время разбора.

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer потребления cpu](https://direct.yandex.ru/logviewer/#~(logType~'trace~form~(fields~(~'log_time~'service~'method~'tags~'trace_id~'span_id~'ela~'cpu_user~'profile)~conditions~(method~'bids.get~cpu_user~'*3e1)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [График с перцентилем](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=common-metrics&l.host=CLUSTER&l.sensor=traceLogTimeSpent&l.monitoring_method=grid.api.BannersQuery&graph=auto&transform=moving_average&movingWindow=1h&overLinesTransform=WEIGHTED_PERCENTILE&percentiles=95&b=1w&e=&l.bin=*)
- [Пример конфигурации алерта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogCpu-direct.intapi.json)

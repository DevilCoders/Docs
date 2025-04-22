# Алерты потребления памяти запросами lifeline_traceLogMem

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMem-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMem-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMem-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMem-direct.web.perl)

[Алерт в solomon для graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMem-direct.web.grid.api)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMem-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogMem-direct.web.java)

## Описание { #description }

Алерты на потребление памяти. Строится на основе трейс логов. Срабатывает при превышении перцентиля, описанного в [конфиге сервиса](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogDbWriteCalls-direct.intapi.json?rev=r8120867#L6), перцентиля заданного порога.
Остается гореть в течение трех-четырех часов после срабатывания.

## Диагностика { #diagnostics }
{% include [links](_includes/release-threshold.md) %}

### Другое
1. Еще одной возможной причиной пробития порога могут быть большие клиенты, которые сделали много запросов с большим количеством данных. Задаутаймить проверку или поменять пороги.
1. Если порог пробит долгое время и нет кандидата на источник, то проверить по [инструкции](../../../incidents/how-to-report.md) можно ли считать проблему аварией, если нет, то завести задачу в zbp. Повысить порог на время разбора.

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer большого потребления памяти](https://direct.yandex.ru/logviewer/#~(logType~'trace~form~(fields~(~'log_time~'service~'method~'tags~'trace_id~'span_id~'ela~'cpu_user~'profile)~conditions~(mem~'*3e1000~method~'bids.get)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [График с перцентилем](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=common-metrics&l.host=CLUSTER&l.sensor=traceLogMem&l.monitoring_method=grid.api.BannersQuery&graph=auto&transform=moving_average&movingWindow=1h&overLinesTransform=WEIGHTED_PERCENTILE&percentiles=95&b=1w&e=&l.bin=*)
- [Пример конфигурации алерта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogMem-direct.canvas.json)

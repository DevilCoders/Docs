# Алерты на количество читающих запросов в базу lifeline_traceLogDbReadCalls

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogDbReadCalls-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogDbReadCalls-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogDbReadCalls-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogDbReadCalls-direct.web.perl)

[Алерт в solomon для graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogDbReadCalls-direct.web.grid.api)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogDbReadCalls-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogDbReadCalls-direct.web.java)

## Описание { #description }

Алерты на количество запросов чтения в базу. Строится на основе трейс логов.
Срабатывает при превышении (сейчас 95-го) перцентиля заданного порога.
Остается гореть в течение трех-четырех часов после срабатывания.

## Диагностика { #diagnostics }

{% include [links](_includes/release-threshold.md) %}

### Другое
1. Еще одна возможная причина пробития порога в том, что пришел большой клиент и сделал много запросов с большим количеством данных. Это значит, что в ручке могут быть неоптимальные запросы в базу, количество которых увеличивается от количества данных.
2. Если порог пробит долгое время и нет кандидата на источник, то проверить по [инструкции](../../../incidents/how-to-report.md) можно ли считать проблему аварией, если нет, то завести задачу в zbp. На время починки задаунтаймить или повысить порог в конфиги алерта соответствующего сервиса [пример](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogDbReadCalls-direct.web.grid.api.json)

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [График с перцентилем](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=common-metrics&l.host=CLUSTER&l.sensor=traceLogDbReadCalls&l.monitoring_method=grid.api.BannersQuery&graph=auto&transform=moving_average&movingWindow=1h&overLinesTransform=WEIGHTED_PERCENTILE&percentiles=95&b=1w&e=&l.bin=*)
- [Пример конфига](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogDbReadCalls-direct.intapi.json)

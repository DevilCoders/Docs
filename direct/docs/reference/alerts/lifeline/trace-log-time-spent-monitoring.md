# Алерты времени выполнения lifeline_traceLogTimeSpent

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpent-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpent-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpent-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpent-direct.web.perl)

[Алерт в solomon для graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpent-direct.web.grid.api)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpent-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogTimeSpent-direct.web.java)

## Описание {#description}

Алерты на время выполнения запросов. Строится на основе трейс логов. Срабатывает при превышении перцентиля, описанного в [конфиге сервиса](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogDbWriteCalls-direct.intapi.json?rev=r8120867#L6), перцентиля заданного порога.
Остается гореть в течение трех-четырех часов после срабатывания.

Превышение порога может иметь три причины (что делать — ниже):
- проблемы на стороне Директа
- проблемы на стороне соседних сервисов
- флапы

## Диагностика {#diagnostics}
{% include [links](_includes/release-threshold.md) %}

### Проверить наличие инфраструкурных проблем
1. Если время на получение ответа увеличилось у большого количества не связанных ручек (разные сущности и трейсы), то проверить текущее время выполнения запросов к базе. [Пример yql](https://yql.yandex-team.ru/Operations/YKe6ExJKfbwxERg8vBWSixp1aBrEX4uujt1Eeq6_Xwg=)
   Если да, то задаунтаймить проверку на время починки.
1. Если проблем не нашлось, то смотреть [{#T}](#external-service-problem)

### Проверить время ответа соседних сервисов {#external-service-problem}
Для определения времени ответа соседнего сервиса можно воспользоваться [запросом](https://yql.yandex-team.ru/Operations/YKe6DBJKfbwxERg0RPx-PB5ezNQBprGJUo6RuGBDa3Y=), который выводит 95-ый перцентиль времени ответа показометра.
Для получения данных других сервисов нужно знать его название в трейсе. Его можно найти в логвьювере в колонке profile среди долгих запросов ручки.
1. Если есть информация о работах во внешних сервисах и по [логам](https://direct.yandex.ru/logviewer/#~(logType~'trace~form~(from~'20210419T000000~to~'20210419T235959~fields~(~'log_time~'service~'method~'tags~'trace_id~'span_id~'ela~'cpu_user~'profile)~conditions~(method~'bids.get)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$) видно увеличение времени ответа внешнего сервиса, то задаутаймить проверку на время починки.
2. Если информации о проблемах не обнаружилось, то найти дежурных этого сервиса и узнать есть ли проблемы на их стороне, приложив примеры запросов.
3. Дальше по ситуации

### Другое
1. Еще одна возможная причина пробития порога - флапы, например, пришел большой клиент и сделал много запросов с большим количеством данных или ручка вызывается редко, проверить можно через логвьювер в полезных ссылках. Задаутаймить проверку или поменять пороги.
1. Если порог пробит долгое время и нет кандидата на источник, то проверить по [инструкции](../../../incidents/how-to-report.md) можно ли считать проблему аварией, если нет, то завести задачу в zbp. На время починки задаунтаймить или повысить порог в конфиги алерта соответствующего сервиса [пример](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogTimeSpent-direct.web.java.json)

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer долгих трейс логов](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'*25TraceLogSystemMonitoringJob*25~message~'*25slow_trace_log_in*25keywordbids.get*25)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [LogViewer всех трейс логов ручки](https://direct.yandex.ru/logviewer/#~(logType~'trace~form~(fields~(~'log_time~'service~'method~'tags~'trace_id~'span_id~'ela~'cpu_user~'profile)~conditions~(method~'keywordbids.get)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [LogViewer количества вызовов ручки](https://direct.yandex.ru/logviewer/#~(logType~'trace~form~(fields~(~'log_time)~conditions~(method~'keywordbids.get)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false~showStats~true~sortByCount~false~logTimeGroupBy~'HOUR))$)
- [График с перцентилем](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=common-metrics&l.host=CLUSTER&l.sensor=traceLogTimeSpent&l.monitoring_method=grid.api.BannersQuery&graph=auto&transform=moving_average&movingWindow=1h&overLinesTransform=WEIGHTED_PERCENTILE&percentiles=95&b=1w&e=&l.bin=*)
- [Пример конфигурации алерта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/threshold/traceLogTimeSpent-direct.web.java.json)

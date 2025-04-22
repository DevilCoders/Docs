# Мониторинг

## Error booster

У приложения есть свой дашборд в [Error booster](https://wiki.yandex-team.ru/error-booster). Он находится по [этому адресу](https://error.yandex-team.ru/projects/kadavrique).

Ошибки, которые возникают в кадаврике, отправляются в Error booster через [push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client) (топик в [logbroker](https://logbroker.yandex-team.ru/docs) - `market-front-infra/testing/error-booster-test`, `market-front-infra/market-infra-error-booster`).

Список доступных метаданных ошибок в additional:

- additional.sandboxTaskId
- additional.testMethod
- additional.testType
- additional.package
- additional.repo
- additional.branch
- additional.testClass
- additional.suite
- additional.ticket
- additional.resultFormat
- additional.severity
- additional.feature
- additional.host
- additional.thread
- additional.kadavrSessionId
- additional.issue
- additional.story
- additional.testId

## Метрики

Метрики сервиса можно посмотреть [здесь](https://monitoring.yandex-team.ru/projects/market-front/dashboards/monlu64brmostgmtcerl?from=now-1d&to=now&refresh=60000&p.var_env=production&p.var_dc%5B0%5D=%2A&p.var_mock_name%5B0%5D=%2A&p.var_target_service%5B0%5D=%2A&p.var_quant=0.95&p.var_m_avg=30m&p.var_period=five_min).

Метрики redis'a, который используется сервисом, можно найти [здесь](https://monitoring.yandex-team.ru/projects/internal-mdb/dashboards/mon9obabhq5tvnrpcj0g/view?refresh=15000&p.cid=mdb6f682ar11r1r7ff49&from=now-1h&to=now).

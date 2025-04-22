# Проверки счётчиков и метрик. Документация разработчика

Общая информация по теме находится в [основном разделе документации](./structure.md).

## Troubleshooting

### Собрать core dump для демона метрик

В дочерних задачах `SANDBOX_CI_HERMIONE_SUBTASK` задайте параметру `coredump_filter_pattern` значение `.*`, чтобы в
ресурсах задачи сохранились все обнаруженные core dump'ы. Предлагается сохранять все, так как название бинарника уже менялось.
На момент написания бинарник называется `HttpServer`.

Для упрощения: [FEI-21283: sandbox_ci_hermione: добавить параметр coredump_filter_pattern для передачи в сабтаски](https://st.yandex-team.ru/FEI-21283)

### Получить тела запросов к демону метрик

Плагин hermione-get-counters по умолчанию записывает тела неуспешных запросов на расчет метрик к демону метрик в папку
`.yandex-int/logs`, которая сохраняется в большинстве задач в качестве ресурса, по пути `.yandex-int/logs/calc-metrics-daemon`.

Если для дебага (например, плавающей проблемы) нужны тела всех сделанных в демон метрик запросов, можно запустить тесты
с переменной среды окружения `ARCHON_METRICS_FETCHER_PREPARE_LOGS_ALL: true`. 
Это позволит записать все запросы, в том числе, ретраи.

## Мониторинги

### Отставание версии демона метрик от продакшена

Мониторинг отставания реализован при помощи [шедулера в Sandbox](https://sandbox.yandex-team.ru/scheduler/24212/view).

Раз в сутки запускается задача `MONITOR_METRICS_DAEMON_IN_PROJECTS`, которая по известным ей сервисам считает отставания
версии демона от продакшена в днях и отправляет эти данные в stat для построения [графика](https://datalens.yandex-team.ru/preview/bj7rqm4wc16g6-metrics-daemon-lags).
При превышении отставания на 14 дней отправляется оповещение в `INFRADUTY`.

Автообновление поддержано в следующих проектах:

- web4: [задачи для дежурного сервиса](https://st.yandex-team.ru/issues/?_q=Queue%3A+SERP+Tags%3A+metrics-daemon-update++%22Sort+by%22%3A+Created+DESC)
- fiji: [задачи для дежурного сервиса](https://st.yandex-team.ru/issues/?_q=Queue%3A+SAKHALIN+Tags%3A+metrics-daemon-update++%22Sort+by%22%3A+Created+DESC)

Если в Sandbox-задаче ошибка `В следующих проектах устаревший демон метрик`, то нужно позвать в тикет @fenice и
замьютить мониторинг: выставить [alert_on_old_version](https://a.yandex-team.ru/arc_vcs/sandbox/projects/sandbox_ci/counters_metrics/projects.py?rev=6c343738daa12c6b4bb824c395569d4efcff9fe5#L12) соответствующего проекта в `False` и закоммитить.

Для упрощения: [FEI-21272: metrics: возможность мьютить мониторинг отставания демона метрик от прода без коммита в SB задачу](https://st.yandex-team.ru/FEI-21272).

Если задача упала с любой другой ошибкой, попробовать её расследовать. В случае неудачи позвать @fenice.

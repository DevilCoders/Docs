# Проверки счётчиков и метрик. Подключение

Будем рассматривать подключение на примере сервиса, использующего в качестве девсервера [kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html) и преднастроенные команды `archon-renderer-devserver-command`/`archon-hermione`. При возникновении проблем и вопросов приходите в [INFRADUTY](https://wiki.yandex-team.ru/infraduty/).


## 0. Определить, какие логи необходимы

Список необходимых логов зависит от того, какие проверки нужно делать в тестах сервиса.

Если необходимы проверки серверных счётчиков, то нужны логи серверных счётчиков - `blockstat` (aka `baobab`).

Если необходимы проверки клиентских счётчиков, то нужны логи клиентских счётчиков - `redir`. 

Если необходимы проверки метрик, то у аналитиков нужно узнать, какие сырые логи требуются для расчёта метрик качества сервиса. В настоящий момент реализована поддержка метрик на основе логов `blockstat`, `redir`, `reqans`. Если для ваших проверок требуются иные логи, приходите в [INFRADUTY](https://wiki.yandex-team.ru/infraduty/) для обсуждения.


## 1. Настроить запись сырых логов

### 1.1. Настроить запись `blockstat`

Логи пишутся `renderer`'ом в `~/.yandex-int/logs/rr`.

Настройка не требуется.

### 1.2. Настроить запись `redir`

Логи пишутся [clickdaemon](https://wiki.yandex-team.ru/logs/clickdaemon/)'ом в `~/.yandex-int/logs/clickdaemon`.

Требуется убедиться, что запросы на `/clck` будут приходить в локально поднятый clickdaemon. Для этого:

1. Убедиться, что шаблоны на девсервере в качестве CLCK-хоста используют хост девсервера. Сервис может брать его из данных (например, из заголовков запроса), которые сохраняются в дампе при его записи. Тогда нужно реализовать подходящий способ переопределения.
2. Добавить в [конфиг kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#format-konfiguratsionnogo-faila) обработку роута `/clck`, и в обработку добавить мидлвар [counter](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#counter), перенаправляющий запросы в локально запущенный clickdaemon.

### 1.3. Настроить запись `reqans`

Логи пишутся в дампы при их сохранении.

Требуется убедиться, что при походе за данными Renderer получит reqans. Для этого:

1. Убедиться, что при запросе данных с ожидаемым параметром выдаётся `reqans`. Обычно используют `dump=reqans`.
2. Добавить этот параметр в список параметров, с которыми делается запрос за данными в основном роуте сервиса.


## 2. Настроить актуализацию `reqId`

Актуализация требуется для того, чтобы все счётчики записались с одинаковым уникальным `reqId`, по которому впоследствии будут собираться записи из логов.

Для этого в обработку роутов, в контенте которых встречается `reqId`, необходимо добавить соответствующий мидлвар для подмены reqId ([AppHost](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#replacereqidapphost)/[не AppHost](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#replacereqidregular)). Мидлвар должен находиться в цепочке после получения данных `cacheReader`/`getData` и до `render`.


## 3. Настроить сбор сырых логов в хранилище

Хранилищем логов выступает компонент [metrics-fetcher](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-metrics-fetcher.html). Для того, чтобы логи собирались, необходимо:

1. Убедиться, что компонент `archon-metrics-fetcher` подключён в команду запуска девсервера и тестов, и он участвует в запуске. При использовании [archon-renderer-devserver-command](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-renderer-devserver-command.html) и/или [archon-hermione](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-hermione.html) необходимо добавить ключ `--kotik-counters`, если нужны только проверки счётчиков, или `--kotik-metrics`, если нужны проверки и счётчиков, и метрик.
2. Сформировать конфигурационный файл с настройками сбора логов. Детали настройки логов ниже.

### 3.1. Настроить сбор логов `blockstat`

В [конфигурации `metrics-fetcher`](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-metrics-fetcher.html#konfiguratsiia) в поле `logs.blockstat.fileNames` необходимо указать список файлов, в которые сервис пишет серверные логи.

### 3.2. Настроить сбор логов `redir`

В [конфигурации `metrics-fetcher`](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-metrics-fetcher.html#konfiguratsiia) в поле `logs.redir.fileNames` необходимо указать список файлов, в которые сервис пишет серверные логи.

### 3.3. Настроить сбор логов `reqans`

Если для сервиса требуется расчёт метрик качества, и для расчёта необходим `reqans` лог, то в [конфигурации `metrics-fetcher`](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-metrics-fetcher.html#konfiguratsiia) нужно выставить в `true` поле `logs.reqans.needed` и в поле `logs.reqans.daemonRequestName` указать, через какое поле запроса к [демону метрик, calc_metrics_daemon](https://wiki.yandex-team.ru/logs/calcmetricsdaemon/) нужно его передавать.


## 4. Подключить hermione-команды для проверки счётчиков и метрик

Для получения собранных логов и рассчитанных метрик и сверки их с ожидаемыми значениями реализован плагин [hermione-get-counters](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/hermione-get-counters.html). Инструкции по настройке есть [в документации плагина](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/hermione-get-counters.html#dlia-kotik).

Кроме точечных проверок метрик в определённых тестах можно также настроить массовую проверку метрик во всех тестах с сохранением эталонных значений в файлы рядом с тестами при помощи плагина [hermione-assert-metrics](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/hermione-assert-metrics.html).

Готово!

## Релевантные ссылки

- [clickdaemon](https://wiki.yandex-team.ru/logs/clickdaemon/)
- [демон метрик, calc_metrics_daemon](https://wiki.yandex-team.ru/logs/calcmetricsdaemon/)
- [kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html)
- [archon-renderer-devserver-command](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-renderer-devserver-command.html)
- [archon-hermione](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-hermione.html)
- [archon-metrics-fetcher](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-metrics-fetcher.html)
- [hermione-get-counters](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/hermione-get-counters.html)
- [hermione-assert-metrics](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/hermione-assert-metrics.html)

# Секция awacs

- [Секция sections](#секция-sections)
- [Секция alertsets](#секция-alertsets)
    - [Алиасы для сигналов](#алиасы-для-сигналов)
    - [Пояснение про виды ошибок](#пояснение-про-виды-ошибок)

Пример:
```yaml
awacs:
  sections:
    maps.yandex.net.service_total: default

  alertsets:
    default:
      settings:
        notifications: [chat, team]  # Кому отправлять уведомления
      alerts:
        http_5xx:
          signal: '%5xx_perc'  # Процент пятисоток
          warn: 0.1  # Статус WARN, если больше 0.1%
          crit: 2  # Статус CRIT, если больше 2%
```

## Секция sections

Определяет соответствие `секция awacs-конфига` -> `набор алертов`.

Формат: `<имя_неймспейса>.<report_uuid_секции>: <имя_алертсета>`

Например, для неймспейса https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/daas-farm.yandex.net/show/
нужно указать имя `daas-farm.yandex.net`.

После имени неймспейса и точки нужно указать `uuid`, который передан в модуль `report` в конфиге нужного апстрима.
Обычно это выглядит так:

```yaml
  modules:
    - report:
        ranges: default
        uuid: my-section-uuid
```

:exclamation: Список доступных `uuid` секций можно увидеть во вкладке `Monitoring` на странице неймспейса.

> :bulb: По умолчанию создается секция `service_total`, которая собирает статистику **со всех апстримов балансера**.
  Если вам не нужно разбивать мониторинги по апстримам/ДЦ/доменам/роутам и т.д., можете использовать ее.

## Секция alertsets

Базовый формат описан [тут](./common.md#Секция-alertsets).

> :bulb: В своих сигналах можно использовать плейсхолдер `{uuid}`, который будет заменен на `uuid` секции.
  Это позволит переиспользовать алертсет к нескольким секциям неймспейса(-ов) без изменения сигнала.
  Например: `signal: 'balancer_report-report-{uuid}-ka_summ'`

Для удобства в Monitorado заведены алиасы для наиболее полезных сигналов.
Их названия начинаются с символа `%`.

### Алиасы для сигналов

Алиас | Сигнал                                                                                                                                                                                                                                                          | Описание
--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------
%5xx | div(balancer_report-report-{uuid}-outgoing_5xx_summ, normal())                                                                                                                                                                                                  | Количество ответов с кодами вида 5xx в секунду
%5xx_perc | or(perc(balancer_report-report-{uuid}-outgoing_5xx_summ, balancer_report-report-{uuid}-requests_summ), 0)                                                                                                                                                       | Процент ответов с кодами вида 5xx
%5xx (uuid=service_total) | div(diff(balancer_report-report-service_total-outgoing_5xx_summ, or(balancer_report-report-announce_check-outgoing_5xx_summ, 0)), normal())                                                                                                                     | Количество ответов с кодами вида 5xx (без учета announce check 5xx) в секунду
%5xx_perc (uuid=service_total) | or(perc(diff(balancer_report-report-service_total-outgoing_5xx_summ, or(balancer_report-report-announce_check-outgoing_5xx_summ, 0)), diff(balancer_report-report-service_total-requests_summ, or(balancer_report-report-announce_check-requests_summ, 0))), 0) | Процент ответов с кодами вида 5xx (без учета announce check 5xx)
%4xx | div(balancer_report-report-{uuid}-outgoing_4xx_summ, normal())                                                                                                                                                                                                  | Количество ответов с кодами вида 4xx в секунду
%4xx_perc | or(perc(balancer_report-report-{uuid}-outgoing_4xx_summ, balancer_report-report-{uuid}-requests_summ), 0)                                                                                                                                                       | Процент ответов с кодами вида 4xx
%404_perc | or(perc(balancer_report-report-{uuid}-outgoing_404_summ, balancer_report-report-{uuid}-requests_summ), 0)                                                                                                                                                       | Процент ответов с кодом 404
%4xx_err_perc | or(perc(diff(balancer_report-report-{uuid}-outgoing_4xx_summ, balancer_report-report-{uuid}-outgoing_404_summ), balancer_report-report-{uuid}-requests_summ), 0)                                                                                                | Процент ответов с кодами вида 4xx, где 4xx не равно 404
%fail | div(balancer_report-report-{uuid}-fail_summ, normal())                                                                                                                                                                                                          | Количество безуспешных ответов из-за ошибок на стороне клиента или бэкенда в секунду
%fail_perc | or(perc(balancer_report-report-{uuid}-fail_summ, balancer_report-report-{uuid}-requests_summ), 0)                                                                                                                                                               | Процент безуспешных ответов из-за ошибок на стороне клиента или бэкенда
%backend_fail_perc | or(perc(balancer_report-report-{uuid}-backend_fail_summ, balancer_report-report-{uuid}-requests_summ), 0)                                                                                                                                                       | Процент безуспешных ответов из-за ошибок на стороне сервера
%client_fail_perc | or(perc(balancer_report-report-{uuid}-client_fail_summ, balancer_report-report-{uuid}-requests_summ), 0)                                                                                                                                                        | Процент безуспешных ответов из-за ошибок на стороне клиента
%timings_p95 | or(quant(balancer_report-report-{uuid}-processing_time_hgram, 95), 0)                                                                                                                                                                                           | 95 перцентиль времен ответа __в секундах__
%timings_p99 | or(quant(balancer_report-report-{uuid}-processing_time_hgram, 99), 0)                                                                                                                                                                                           | 99 перцентиль времен ответа __в секундах__
%timings_p(N) | or(quant(balancer_report-report-{uuid}-processing_time_hgram, N), 0)                                                                                                                                                                                            | N-ый перцентиль времен ответа __в секундах__, где N от 1 до 99

### Пояснение про виды ошибок
1. client_fail это ошибки на стороне клиента. Чаще всего говорит, что соединение порвалось во время отправки запроса или получения ответа. У внешнего сервиса всегда будет
небольшой фон таких ошибок.
2. backend_fail это фатальная ошибка на стороне бэкенда. Происходит, когда кончились перезапросы в бэкенда под балансером (или время на них), но ответ так и не был получен, после чего выполняется секция on_error.
3. fail = client_fail + backend_fail.
4. 5xx - пятисотка. Не совсем очевидно коррелирует с backend_fail. В зависимости от того, как в balancer2 настроены on_error, fail_on_5xx, status_code_blacklist и return_last_5xx, может как совпадать с 5xx, так и не совпадать, потому что
в некоторых конфигурациях балансер будет просто разрывать соединение при любой ошибке.

Вывод - крайне желательно мониторить **и backend_fail, и 5xx**. Остальное - по необходимости.


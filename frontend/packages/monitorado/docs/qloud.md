# Секция qloud

Включает две подсекции:

- [Секция apps](#секция-apps)
    - [Маска компонента](#маска-компонента)
- [Секция alertsets](#секция-alertsets)
    - [Алиасы для сигналов](#алиасы-для-сигналов)
- [Нюансы](#нюансы)

Пример:
```yaml
qloud:
  # Пишем полные имена своих компонентов
  apps:
    # * означает "любое приложение в проекте maps"
    maps.*.production.www: default

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

## Секция apps

Определяет соответствие `компонент в Qloud` -> `набор алертов`.
Формат: `<маска_компонента>: <имя_алертсета>`

Пример:
```yaml
apps:
  education.ege-api.production.api: first
  education.kelvin-api.production: second
  doc.*.production.www: third
```

### Маска компонента

Имеет следующий формат: `<имя_проекта>.<имя_приложения>.<имя_окружения>.<имя_компонента>`.
Для всего, что идет после проекта, поддерживается маска `*`, причем завершающие `*` можно опустить.

Примеры:
1. `prj.app.env.comp` - идентифицирует ровно одну компоненту
1. `prj` (эквивалетно `prj.*.*.*`) - все компоненты в проекте `prj`
1. `prj.app` (эквивалетно `prj.app.*.*`) - все компоненты внутри всех окружений внутри приложения `app` проекта `prj`
1. `prj.app.env` (эквивалетно `prj.app.env.*`) - по аналогии
1. `prj.*.env.comp` - компоненты с именем `comp` внутри окружения `env` внутри всех приложений проекта `prj`

## Секция alertsets

Базовый формат описан [тут](./common.md#Секция-alertsets).

В поле `signal` можно использовать имена метрик, которые описаны в [документации](https://doc.qloud.yandex-team.ru/doc/dashboards#metrics).
:warning: В одном сигнале нельзя одновременно использовать метрики с балансеров (префикс `push-`) и метрики с хостов (`portoinst-`, `unistat-`).

Для удобства в Monitorado заведены алиасы для наиболее полезных сигналов.
Их названия начинаются с символа `%`.

### Алиасы для сигналов

#### HTTP-метрики

Алиас | Сигнал | Описание
--------|--------|---------
%5xx_perc | or(perc(push-response_5xx_summ, push-requests_summ), 0) | Процент ответов с кодом 5xx
%4xx_perc | or(perc(push-response_4xx_summ, push-requests_summ), 0) | Процент ответов с кодом 4xx
%499_perc | or(perc(push-http_499_summ, push-requests_summ), 0) | Процент ответов с кодом 499
%timings_p95 | or(quant(push-time_hgram,95), 0) | 95 перцентиль времен ответа __в секундах__
%timings_p99 | or(quant(push-time_hgram,99), 0) | 99 перцентиль времен ответа __в секундах__

#### Системные метрики

Алиас | Сигнал | Описание
--------|--------|---------
%cpu_perc | perc(portoinst-cpu_usage_cores_tmmv, portoinst-cpu_guarantee_cores_tmmv) | Процент потребления CPU относительно гарантированного лимита (может быть больше 100)
%mem_perc | perc(portoinst-memory_usage_gb_tmmv, portoinst-memory_guarantee_gb_tmmv) | Процент потребления памяти относительно гарантированного лимита (может быть больше 100)
%net_perc | perc(sum(portoinst-net_mb_summ, portoinst-net_rx_mb_summ), portoinst-net_limit_mb_summ) | Процент использования сети
%max_mem_perc | perc(portoinst-memory_usage_gb_txxx, div(portoinst-memory_guarantee_gb_tmmv, counter-instance_tmmv)) | Процент потребления памяти (максимальный по инстансам)
%max_disk_perc | or(portoinst-volume_root_usage_perc_txxx, 0) | Процент потребления диска (максимальный по инстансам)

#### Метрики логов

Алиас | Сигнал | Описание
--------|--------|---------
%logs_per_sec | div(push-messages_summ, 5) | Количество сообщений в секунду
%logs_drop_perc | perc(push-drop_summ, push-messages_summ) | Процент отброшенных из-за квоты сообщений
%logs_fail_perc | perc(push-fail_summ, push-messages_summ) | Процент сообщений, который не получилось распарсить 
%logs_mb_per_sec | div(conv(push-bytes_summ, Mi), normal()) | Количество логов в секунду в мегабитах
%logs_level_warn_per_sec | div(push-level_WARN_summ, normal()) | Количество WARN-сообщений в секунду
%logs_level_warn_perc | perc(push-level_WARN_summ, push-messages_summ) | Процент WARN-сообщений
%logs_level_err_per_sec | div(push-level_ERROR_summ, normal()) | Количество ERROR-сообщений в секунду
%logs_level_err_perc | perc(push-level_ERROR_summ, push-messages_summ) | Процент ERROR-сообщений

## :warning: Нюансы

1. (Актуально для версии <= 3.1.0) Значение метрики = сумма значений с конкретного набора юнитов компонента (например: `frontend-1, frontend-2, ... frontend-k`).
   Если вы увеличиваете количество инстансов, мониторинги нужно обновить, иначе значения с новых инстансов не будут учитываться.

1. Значения HTTP-метрик забираются с конкретного набора балансеров (например: `common, L7, my-custom-balancer`).
   Если вы добавляете в окружение домен на новом балансере, мониторинги нужно обновить, иначе значения с него не будут учитываться.

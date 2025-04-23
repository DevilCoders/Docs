# Секция deploy

- [Секция objects](#секция-objects)
- [Секция alertsets](#секция-alertsets)
    - [Алиасы для сигналов](#алиасы-для-сигналов)

Пример:
```yaml
deploy:
  objects:
    stage:maps_backend: default
    deploy_unit:maps_backend.backend: default

  alertsets:
    default:
      settings:
        notifications: [chat, team]  # Кому отправлять уведомления
      alerts:
        cpu_usage:
          signal: '%cpu_perc(99)'  # 99-ый перцентиль потребления CPU
          warn: 60  # Статус WARN, если больше 60%
          crit: 80  # Статус CRIT, если больше 80%
        app_counter:
          signal: 'unistat-my_custom_counter_summ'  # Произвольный unistat-сигнал
          crit: 100
          tags:
            itype: custom-itype  # При необходимости можно переопределить itype для unistat-ручки
```

## Секция objects

Определяет соответствие `сущность в Деплое` -> `набор алертов`.

На данный момент поддерживаются следующие типы:

1. Deploy unit
   Формат: `deploy_unit:<имя_стейджа>.<имя_du>`.
   Метрики агрегируются по всем подам.
1. Stage
   Формат: `stage:<имя_стейджа>`.
   В этом случае метрики будут агрегироваться по всем подам всех деплой юнитов.
   > :bulb: Необходимо, чтобы у всех деплой юнитов был настроен один itype

> :bulb: Если itype для unistat-ручки явно задан и отличается от itype деплой юнита, его нужно задать явно,
  как в примере выше

## Секция alertsets

Базовый формат описан [тут](./common.md#Секция-alertsets).

Для удобства в Monitorado заведены алиасы наиболее полезных сигналов.
Их имена начинаются с символа `%`.

### Алиасы для сигналов

Алиас | Сигнал | Описание
--------|---------|---------
%cpu_perc(N) | quant(portoinst-cpu_limit_usage_perc_hgram, N) | N-ый перцентиль процента потребления CPU, где N либо число от 1 до 99, либо max
%cpu_perc_avg | havg(portoinst-cpu_limit_usage_perc_hgram) | Средний процент потребления CPU
%cpu_wait(N) | quant(portoinst-cpu_wait_slot_hgram, N) | N-ый перцентиль времени ожидания процессов в очереди, где N либо число от 1 до 99, либо max. Значение больше 1 обычно говорит о нехватке CPU
%cpu_wait_avg | havg(portoinst-cpu_wait_slot_hgram) | Среднее время ожидания процессов в очереди. Значение больше 1 обычно говорит о нехватке CPU
%anon_mem_perc(N) | quant(portoinst-anon_limit_usage_perc_hgram, N) | N-ый перцентиль процента потребления памяти (anon), где N либо число от 1 до 99, либо max
%anon_mem_perc_avg | havg(portoinst-anon_limit_usage_perc_hgram) | Средний процент потребления памяти (anon)
%mem_perc(N) | quant(portoinst-memory_limit_usage_perc_hgram, N) | N-ый перцентиль процента потребления памяти **с учетом файловых кэшей**. Если вы не разбираетесь в памяти, лучше использовать %anon_mem_*
%mem_perc_avg | havg(portoinst-memory_limit_usage_perc_hgram) | Средний процент потребления памяти **с учетом файловых кэшей**. Если вы не разбираетесь в памяти, лучше использовать %anon_mem_* 
%net_perc_avg | perc(sum(portoinst-net_tx_mb_summ, portoinst-net_rx_mb_summ),portoinst-net_limit_mb_summ) | Средний процент потребления сети. Необходимо, чтобы у деплой юнита был задан `Network bandwidth`

### Нюансы
1. Ресурсные метрики считаются для всего пода целиком, включая подконтейнеры для TVM и логов, поэтому %cpu_perc* может быть низким даже в случае, когда
   ваше приложение уперлось в лимит. Поэтому категорически рекомендуется сделать пороги пониже и настроить алерт на %cpu_wait*
2. При установке лимитов на боксы и поды также стоит это учитывать

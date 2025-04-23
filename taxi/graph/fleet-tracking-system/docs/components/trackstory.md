# Сервис хранения позиций - trackstory


## Конфигурация

Конфигурация для хранения описывается вот такой схемой

{% cut "Схема притягивателя" %}

{% code '../yaml/config_internal/trackstory.yaml' lang=yaml %}

{% endcut %}

Конфиг для сервиса хранения позиций описывает какие позиции надо хранить в
горячем кеше и сколько времени их там надо хранить.

Конфиг по сути описывается двумя основными секциями:
1. Что читать
2. Сколько хранить, per-source.

Все каналы из ```input-channels``` сливаются (вирутально) в один большой поток,
и позиции записываются в горячее хранилище. Позиции одного источника
сгруппированны.
К каждому источнику применяются свои настройки хранения. Тем самым, например,
можно хранить 'Verified' 7 часов, 'Adjusted' - 15 минут, а 'AndroidGps' - последние 3 позиции


Вот пример простого конфига trackstory - храним один источник 15 минут.

{% if has_jsonpath %}

{% code '../yaml/config_internal/trackstory.yaml' lang='yaml' jsonpath='$.definitions.TrackstoryPipelineConfig.examples.plain_modern_channels' %}

{% else %}

```yaml
input-channels:
  - channel: raw_driver_positions
  - channel: raw_pedestrian_positions
shorttracks:
  - latest-position-ttl: 30000
    shorttrack-ttl: 900
    sources: [ Verified ]
```

{% endif %}

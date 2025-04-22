# Monitoring Utils

Либа упрощает добавление jvm метрик в  соломон через prometheus метрики


## Как использовать

### Настройка solomon-agent

* Добавить PEERDIR на либу в ya.make
* Создать сервис в соломоне ([Пример](https://solomon.yandex-team.ru/admin/projects/market-ir/services/market-ir_smartmatcher_meta))
* Создать кластера в соломоне ([Пример](https://solomon.yandex-team.ru/admin/projects/market-ir/clusters/market-ir_smartmatcher-shard-prod))
* Связать кастера и сервис с помощью шардов в соломоне
* Добавить конфиг соломон агента в проект, указав сервис, созданный ранее ([Пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/ir/smartmatcher/smartmatcher-meta/src/main/tmpl/conf/solomon-agent/service.d/micrometer-prometheus.conf))


### Тайминг кастомных методов

* Добавить аспект на профилируемый метод, в Around методе вызвать MetricUtils.countAndTime(pjp) ([Пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/ir/smartmatcher/smartmatcher-meta/src/main/java/ru/yandex/market/ir/smartmatcher/meta/monitoring_aspect/ProfilerAspect.java))

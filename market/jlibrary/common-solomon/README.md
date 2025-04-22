# common-solomon
Библиотека для подсчета и отправки метрик в [Solomon](https://wiki.yandex-team.ru/solomon/)\
Используются две модели отправки метрик: pull и push

## Pull модель
Про [pull](https://wiki.yandex-team.ru/mbi/development/howto/mbi-solomon/) модель

## Push модель
Используется для отправки jvm и jmx метрик\
Для jmx метрик, если посчитанное значение равно `null` или после инициализации отсутствует один из бинов или атрибутов бина, то бросается исключение\
Формат лейблов для jmx метрик: sensor - имя атрибута, domain - домен бина, propertyName - propertyValue

__Пример использования__
```
MetricsProvider jvmRuntimeMetrics = new JvmRuntimeMetrics();
SolomonPusher solomonPusher = new SolomonPusher();
MetricsPusher metricsPusher = new MetricsPusher(solomonPusher, "project", "cluster", "service", 1, Collections.singletonList(jvmRuntimeMetrics));
metricsPusher.pushMetrics();
```

[MetricsProvider](src/main/java/ru/yandex/market/mbi/web/solomon/common/MetricsProvider.java) – хранит метрики в виде листа [PushMetric](src/main/java/ru/yandex/market/mbi/web/solomon/common/PushMetric.java) и собирает их в лист сенсоров\
[SolomonPusher](https://a.yandex-team.ru/arc/trunk/arcadia/iceberg/inside-solomon/src/main/java/ru/yandex/inside/solomon/pusher/SolomonPusher.java) – Push API для отправки метрик в [Solomon](https://wiki.yandex-team.ru/solomon/)\
[MetricsPusher](src/main/java/ru/yandex/market/mbi/web/solomon/push/MetricsPusher.java) – принимает [SolomonPusher](https://a.yandex-team.ru/arc/trunk/arcadia/iceberg/inside-solomon/src/main/java/ru/yandex/inside/solomon/pusher/SolomonPusher.java),
название проекта, кластера и сервиса, колличество потоков для отправки метрик и лист метрик. Предоставляет возможность отправить нужные метрики в [Solomon](https://wiki.yandex-team.ru/solomon/)

## Метрики
По Push API отправляются следующие метрики:
[метрики потоков](src/main/java/ru/yandex/market/mbi/web/solomon/metrics/JvmThreadMetricsProvider.java),
[runtime](src/main/java/ru/yandex/market/mbi/web/solomon/metrics/JvmRuntimeMetricsProvider.java),
[памяти](src/main/java/ru/yandex/market/mbi/web/solomon/metrics/JvmMemoryMetricsProvider.java),
[сборщика мусора](src/main/java/ru/yandex/market/mbi/web/solomon/metrics/JvmGcMetricsProvider.java),
[jmx](src/main/java/ru/yandex/market/mbi/web/solomon/metrics/JmxMetricsProvider.java)\
Для сбора [Jmx метрик](src/main/java/ru/yandex/market/mbi/web/solomon/metrics/JmxMetricsProvider.java) нужно передать в конструктор конфиг в виде мапы: название бина в сет атрибутов этого бина

Т.к. после отдачи jvm-метрик они удаляются из памяти, чтобы фетчер соломона чувствовал себя комфортно, рекомендуется использовать [solomon agent](https://wiki.yandex-team.ru/Solomon/agent/).\
Для этого нужно создать конфиг для него, например как [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/mbi/jvm-solomon-agent-testing).\
Затем для него нужно создать сервис в админке Solomon'a с названием таким же, как и в конфиге.\
Создать ресурс можно с помощью sandbox таски, например можно склоинровать любую из mbi'ных тасок.\
Таски:
* [mbi-production](https://sandbox.yandex-team.ru/task/707133063/view)
* [mbi-billing-production](https://sandbox.yandex-team.ru/task/708007133/view)
* [mbi-testing](https://sandbox.yandex-team.ru/task/702585677/view)
* [mbi-billing-testing](https://sandbox.yandex-team.ru/task/703573957/view)

## Доступы для API
[Как заказать](https://wiki.yandex-team.ru/solomon/howtostart/#access)

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)

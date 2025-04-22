# Tape

Использует [tape](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/tape) (минималистичная локальная 'нирвана') для запуска вычислений. TapeBackend благодаря прямому общения с сервисами, дает возможность запускать локальную версию кода, а также реализовать локальное тестирование с помощью локальных сервисов (YT, YQL). Также поскольку tape запускается на локальной машине и не требует релизов операций, то его можно быстрее расширять новыми действиями

## Пример

{% cut "train_catboost.yaml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/train_catboost.yaml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}

{% include notitle [train_catboost_draw](../_includes/demonstration/train_catboost_tape.md) %}

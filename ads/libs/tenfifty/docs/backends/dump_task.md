# Dump task

DumpTaskBackend может построить описание графа с помощью [yaml-конфигов](../configuration/parser.md) tenfifty, это может быть полезно при переезде с других способов конфигурирования ML-пайплайнов. Сначала строим tenfifty граф через [python-api](../configuration/api.md), а затем используем DumpTaskBackend как "переводчика".

## Пример

{% cut "train_catboost.yaml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/train_catboost.yaml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}

{% include notitle [train_catboost_draw](../_includes/demonstration/train_catboost_dump_task.md) %}

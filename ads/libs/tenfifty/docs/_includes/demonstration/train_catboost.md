# Учим tlm

Обучаем catboost.

{% cut "train_catboost.yaml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/train_catboost.yaml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}

{% list tabs %}


- Draw

    {% include notitle [train_catboost_draw](train_catboost_draw.md) %}

- Nirvana

    {% include notitle [train_catboost_nirvana](train_catboost_nirvana.md) %}

- Tape

    {% include notitle [train_catboost_tape](train_catboost_tape.md) %}

{% endlist %}

# Draw

Рисующий бэкенд, удобен для отладки перед запуском на "настоящем" бэкенде.

Композитные действия можно разворачивать с помощью дввойного клика.

## Пример

{% cut "train_catboost.yaml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/train_catboost.yaml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}

{% include notitle [train_catboost_draw](../_includes/demonstration/train_catboost_draw.md) %}

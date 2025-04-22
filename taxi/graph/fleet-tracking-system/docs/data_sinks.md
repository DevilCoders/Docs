## Data sinks

Приемники данных (data sinks) - это внешние для системы сущности, куда она умеет
отправлять потоки данных. Их отличие от data streams - они находятся целиком в
user space пользователя, к ним нельзя подцепить наши сервисы.

Мы поддерживаем (планируем поддержать) на данный момент следующие инсталяции:

1. Redis PubSub + flatbuffers
2. Redis PubSub + protobuf
2. Logbroker + JSON


### Примеры и схемы
Вот пример того, как могут описываться пользовательские выходы для нашей
системы.

{% code './yaml/config_internal/data_sinks.yaml' lang='yaml' jsonpath='$.definitions.DataSink.examples.simple_datasink.value' %}
Два потока:
{% code './yaml/config_internal/data_sinks.yaml' lang='yaml' jsonpath='$.definitions.DataSink.examples.datasink_with_filters.value' %}

{% cut 'Схема выхода' %}

{% code './yaml/config_internal/data_sinks.yaml' lang='yaml' jsonpath='$.definitions.DataSink' %}

{% endcut %}

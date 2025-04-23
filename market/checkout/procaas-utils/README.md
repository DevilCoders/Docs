# Утилита для изменения procaas config  и добавление событий#


1. Заполнить  `my.yaml`
1. `project`  - название проекта, используется как префикс для генераций переменных (пример checkouter - ид топика будет checkouter_topic)
1. `logbroker.endpoint` - Инсталяция логброкера (LBKX/logbroker....)
1. `logbroker.prod.topic`  -  Название топика для прода
1. `logbroker.test.topic` - название топика для тестинга
1. `procaas.pipeliene.id` - id Пайплайна в который хотим встроится
1. `procaas.pipeliene.stage` - id Stage после которого нужно добавить отсылку событий
1. `event` - как формировать событие отсылаемое  в ЛБ.
1. Идем `Main` и исправляем путь к исходникам аркадии
1. Запускаем.
1. Коммитим изменения



## Как это работает ##
1. Ищется пайплайн и Стейдж в который ходим дописать.
2. Модифицируются `substitutions/*`  дописывется топик

```yaml

   testic-topic: /market-checkout/production/test-bus
```

3. заполняем данные по логброкерку в procaas

```yaml

    testic-topic:
    tvm-service-name: logbroker
    topic: $testic-topic
    source-id: processing
    global-endpoint: lbkx.logbroker.yandex.net
```

4. Модифицируется пайплайн и добавляется отправка события.

```yaml
    - id: testic_send_event
      handlers:
        - id: testic_send_event
          logbrokers:
            - id: testic_send_event
              alies: testic-topic
              args#xget: /event/payload
```

# LES

- Основная документация по подключению [тут](https://wiki.yandex-team.ru/delivery/development/apps/agregator-logisticheskix-sobytijj/integration/)

## Пару слов
`les-app` – это сервис для обработки входящих через основной транспорт (сейчас это SQS) событий, их правильный роутинг и отправка потребителям через тот же самый транспорт по одному или нескольким направлениями.

## Локальный запуск

### Запуск инфры

```sh
docker-compose -f les-app/dependency-stubs/docker-compose.yml up -d
```

* Посмотреть список очередей:

```sh
docker compose run aws-cli aws --endpoint-url http://alpine-sqs:9324 sqs list-queues
```

* Создать очередь:

```sh
docker compose run aws-cli aws --endpoint-url http://alpine-sqs:9324 sqs create-queue --queue-name simple
```

* Удалить очередь:

```sh
docker compose run aws-cli aws --endpoint-url http://alpine-sqs:9324 \
    sqs delete-queue --queue-url http://alpine-sqs:9324/queue/simple
```

* Очистить очередь:

```sh
docker compose run aws-cli aws --endpoint-url http://alpine-sqs:9324 \
    sqs purge-queue --queue-url http://alpine-sqs:9324/queue/simple
```

### Конфигурация

- **Main class:** ``ru.yandex.market.logistics.les.Les``
- **Copy config**

```sh
cp les-app/src/main/properties.d/local/application.properties.dist les-app/src/main/properties.d/local/application.properties
```

- **Environment variables:**
Нужно получить [yql токен](https://yql.yandex-team.ru/) во вкладке `settings->auth->show-my-token`
```
PROPERTIES_DIR=/path_to_your_arcadia_or_svn_repo/market/logistics/les/les-app/src/main/properties.d;
environment=local;
YDB_TOKEN=YQL_TOKEN
```

### Как подключиться к SQS

- Используй доку к [les-client](https://a.yandex-team.ru/arc_vcs/market/logistics/les/les-client). LES его тоже сам использует

## Примеры

- Java: [les-example-java](https://a.yandex-team.ru/arc_vcs/market/logistics/les/les-example-java)
- пример запроса на отправку события в лес

```sh
curl --location --request POST 'localhost:8081/events/add' \
--header 'Content-Type: application/json' \
--data-raw '{
    "queue": "courier_out",
    "event": {
        "source": "courier",
        "event_id": "102806440",
        "timestamp": "12128729384",
        "event_type": "ORDER_IS_DAMAGED",
        "description": "STRESS_TEST_EVENT",
        "payload": {
            "_type": "ru.yandex.market.logistics.les.CourierOrderEvent",
            "externalOrderId": "7786696",
            "origin": 184697420,
            "rollback": false,
            "requestId": "InTransit",
            "rawEvent": "STRESS_TEST_EVENT"
        }
    }
}'
```

## Администрирование

### Переложить сообщения из одной очереди в другую

По ручке `/events/move` можно переложить сообщения из одной очереди в другую (нужно для возврата сообщений из dlq):

- `from_queue_name` - имя очереди откуда перекладывать сообщения
- `to_queue_name` - имя очереди куда перекладывать сообщения
- `number` - количестов сообщений (default = 100 000)
  Сообщения будут перемещаться, пока `number` не будет перемещено, либо пока не истечет 10 секунд ожидания чтения сообщения из
  очереди `from_queue_name`

Пример:
```sh
curl -X POST http://localhost:8081/events/move \
  -H 'Content-Type: application/json' \
  -d '{"from_queue_name":"test_queue_dlq","to_queue_name":"test_queue","number":3000}'
```


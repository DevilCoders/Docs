# Aeroflot Queue Proxy

Прокси сообщений из очереди IBM MQ аэрофлота в SQS.

## Графики SQS

- testing: https://solomon.yandex-team.ru/?project=kikimr&cluster=sqs&service=kikimr_sqs&host=cluster&dashboard=SQS&l.user=avia&l.queue=testing_aeroflot_order.fifo
- production: https://solomon.yandex-team.ru/?project=kikimr&cluster=sqs&service=kikimr_sqs&host=cluster&dashboard=SQS&l.user=avia&l.queue=aeroflot_order.fifo

## Необходимые перменные окружения
- `AVIA_IBM_MQ_HOST` -- хост для подключения к очереди аэрофлота
- `AVIA_SQS_AEROFLOT_QUEUE_NAME` -- имя очереди в SQS для кликаута
- `AVIA_SQS_AEROFLOT_BOY_QUEUE_NAME` -- имя очереди в SQS для прямого бронирования
- `AVIA_SQS_AEROFLOT_CPA_QUEUE_NAME` -- ещё одна очередь для кликаута. Эту очередь использует CPA коллектор

## Хосты аэрофлота

### testing

- `aeroflot-sabre-ix-mq-kzn.avia.tst.yandex.net` -> `172.21.203.11`
- `aeroflot-sabre-ix-mq-msk.avia.tst.yandex.net` -> `172.20.202.11`

### production

- `aeroflot-sabre-ix-mq-kzn.avia.yandex.net` -> `172.21.200.24`
- `aeroflot-sabre-ix-mq-msk.avia.yandex.net` -> `172.20.200.24`

## Имена очередей в SQS

Данные разделяются по пришедшему маркеру.
Динамические маркеры виды YA******** попадают в очереди кликаута.
Заказы с маркером YANONEN попадают в очередь прямого бронирования

### Кликаут

- devel: `development_kurzhumov_aeroflot_order.fifo`
- testing: `testing_aeroflot_order.fifo`
- production: `aeroflot_order.fifo`

### Прямое бронирование

- testing: `testing_aeroflot_order_boy.fifo`
- production: `aeroflot_order_boy.fifo`

### Кликаут CPA

- testing: `testing_aeroflot_order_cpa.fifo`
- production: `aeroflot_order_cpa.fifo`

## Запуск на dev

```
$ ./travel/avia/aeroflot_queue_proxy/tools/install-dev-requirements.sh
$ cp ./travel/avia/aeroflot_queue_proxy/tools/samples/environments.sh ./travel/avia/aeroflot_queue_proxy/tools/environments.sh
$ vi ./travel/avia/aeroflot_queue_proxy/tools/environments.sh
$ ./travel/avia/aeroflot_queue_proxy/tools/run-dev-consumer.sh
```

### Локальная сборка и запуск docker

```
$ ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/aeroflot_queue_proxy/pkg.json

$ docker run --env-file ./travel/avia/aeroflot_queue_proxy/tools/samples/dev.env -t registry.yandex.net/avia/aeroflot-queue-proxy:...
```

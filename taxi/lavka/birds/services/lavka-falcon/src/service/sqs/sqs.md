[SQS](https://cloud.yandex.ru/services/message-queue) – очередь сообщений. В соколе используется для запуска пайплайна распознавания, обеспечивает однократную обработку
каждого документа.

Для работы с SQS локально потребуется [CLI-утилита](https://wiki.yandex-team.ru/sqs/#cli).

Для локальной разработки по-умолчанию используется общая очередь. Это означает, что если сервис поднят
одновременно у нескольких разработчиков, их инстансы будут писать и читать одну и ту же очередь, и сообщения
могут перемешаться.

Для удобства рекомендуется завести личную очередь при помощи CLI:

```
aws sqs create-queue --queue-name falcon-recognition-dev-<ВАШ ЛОГИН>.fifo --attributes FifoQueue=true --endpoint http://sqs.yandex.net:8771
```

"QueueUrl": "http://sqs.yandex.net:8771/lavka-falcon/falcon-recognition-testing.fifo"

aws sqs create-queue --queue-name falcon-recognition-testing.fifo --attributes FifoQueue=true --endpoint http://sqs.yandex.net:8771

"QueueUrl": "http://sqs.yandex.net:8771/lavka-falcon/falcon-recognition-dev-juliethefox.fifo"
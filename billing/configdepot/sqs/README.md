```bash
ozhegov-x:sqs ozhegov$ AWS_SESSION_TOKEN=*** AWS_SECRET_ACCESS_KEY=unused AWS_ACCESS_KEY_ID=configdepot-dev aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://dev/configdepot-internal.json
{
    "QueueUrl": "http://sqs.yandex.net:8771/configdepot-dev/configdepot-internal.fifo"
}
```

https://wiki.yandex-team.ru/sqs/#cli — в качестве aws_access_key_id использовать configdepot-dev

```bash
ozhegov-x:sqs ozhegov$ aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://dev/configshop-deadletter.json
{
    "QueueUrl": "http://sqs.yandex.net:8771/configshop-dev/configshop-deadletter"
}
ozhegov-x:sqs ozhegov$ aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://dev/configshop.json
{
    "QueueUrl": "http://sqs.yandex.net:8771/configshop-dev/configshop"
}
```

https://wiki.yandex-team.ru/sqs/#cli — в качестве aws_access_key_id использовать configshop-dev

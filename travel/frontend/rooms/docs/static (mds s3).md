https://wiki.yandex-team.ru/mds/

инструмент для управления файлами в s3: https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#nastrojjkaawscli
креденшелы: https://yav.yandex-team.ru/secret/sec-01dz0vaar2bcc2b27rdvnt02mp/explore/versions

Если завели такой конфиг

```
[travel]
aws_access_key_id = XXXXXXXXXXXXX
aws_secret_access_key = YYYYYYYYYYYYYYYYYYYYY
```

то в случае успеха должна выполниться команда

```
aws --profile travel --endpoint-url=http://s3.mds.yandex.net s3 ls s3://travel-frontend
                           PRE /
                           PRE static/
```

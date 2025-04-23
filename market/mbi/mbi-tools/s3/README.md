
## ~/.aws/credentials

[credentials](https://wiki.yandex-team.ru/MBI/secrets/#mdss3) файл настроек для aws-cli

Ключи доступа в этом файле можно использовать с другими клиентами (ex: DragonDisk)

### Пример использования

```bash
aws --endpoint-url=https://s3.mdst.yandex.net s3 --profile dev ls
aws --endpoint-url=https://s3.mdst.yandex.net s3 --profile testing ls
aws --endpoint-url=https://s3.mds.yandex.net s3 --profile prod ls
```

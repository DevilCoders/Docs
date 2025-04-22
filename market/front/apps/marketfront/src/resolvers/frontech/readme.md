# Конфиги s3 от инфраструктуры фронта

Специальные флаги и конфиги, которые мы доставляем, потому что админка конфигов всё ещё на горизонте,
а необходимость поддерживать сервис живым есть сейчас

## Как обновить конфиг?

### Разрешение
Для начала надо получить разрешение от [@grumpy](staff.yandex-team.ru/grumpy) или [@johnvee](staff.yandex-team.ru/johnvee),
т.к. ошибки в конфигах стоят дорого, а в некоторых случаях и намеренно травмируют сервис

### Подготовка
Что ещё понадобится:
- Права на работу с s3. Можно получить в IDM, [по инструкции](https://wiki.yandex-team.ru/market/frontend/jandeks-market-s3-mds/)
- [Любой клиент](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#awscommandlineinterface) для работы с s3

### Пример
Пример того, как с помощью _настроенного_ `aws-cli` можно обновить конфиг

```bash
# ~/.aws/config

[testing]
aws_access_key_id = <YOUR_ACCESS_ID_FOR_TESTING>
aws_secret_access_key = <YOUR_SECRET_ACCESS_KEY_FOR_TESTING>

[prod]
aws_access_key_id = <YOUR_ACCESS_ID_FOR_PRODUCTION>
aws_secret_access_key = <YOUR_SECRET_ACCESS_KEY_FOR_PRODUCTION>

```

```bash
# Заливка файла в тестинг
aws --profile=testing --endpoint-url=http://s3.mdst.yandex.net s3 cp ./degradationFlags.json s3://marketfront/featureToggle/degradationFlags.json

# заливка файла в прод. Изменился profile и endpoint-url
aws --profile=prod --endpoint-url=http://s3.mds.yandex.net s3 cp ./degradationFlags.json s3://marketfront/featureToggle/degradationFlags.json
```

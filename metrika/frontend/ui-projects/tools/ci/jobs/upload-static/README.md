## Загрузка статики на S3

Мы используем яндексовое [S3 API](https://wiki.yandex-team.ru/mds/s3-api) и пакет
[@yandex-int/static-uploader](https://a.yandex-team.ru/arcadia/frontend/packages/static-uploader?rev=r9552033#static-uploader)

`@yandex-int/static-uploader` требует наличия конфига в `.config/static/index.js`, причём этот путь нельзя изменять<br>
Поэтому сейчас в скрипте мы создаём файл конфигов в рантайме, запускаем загрузку статики, а потом его удаляем<br> В
будущем, возможно, откажется от этого пакета в пользу официального
[@aws-sdk/client-s3](https://www.npmjs.com/package/@aws-sdk/client-s3)

Для работы скрипта необходимо передать переменные:

-   SERVICE_NAME — передаётся автоматически через npm скрипт
-   VERSION — версия сервиса, чтобы создать поддерикторию в бакете S3
-   ACCESS_KEY_ID, SECRET_ACCESS_KEY — ключи для доступа к S3

Ключи хранятся в переменных `s3-mds-access-key-id`, `s3-mds-secret-key-id` в
[robot-metrika-test](https://yav.yandex-team.ru/secret/sec-01cq6h5rtj649gg8h94zwqshc8/explore/versions)

### Отладка

Для отладки скрипта можно использовать
[AWS CLI](https://wiki.yandex-team.ru/mds/s3-api/s3-clients#awscommandlineinterface), вот тут
[более подробная дока от Amazon](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html)

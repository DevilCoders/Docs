# Package common-rtc-s3

Пакет для заливки статики в S3

## Использование

```bash
~$ apt install s3cmd # Для mac os brew install s3cmd 
~$ npm install @yandex-taxi/fm-common-rtc-s3
# @param tag — формат x.y.z: --tag=1.0.1
# @param host — s3.mds.yandex.net или s3.mdst.yandex.net для тестового
~$ node_modules/.bin/s3-release --access_key=<key> --secret_key=<key> --service=<fmonorepo-servicename> --version=<tag> --host=<host>
```

## Паблишинг
Для упрощения жизни установите np:
`npm install --global np`

Перейдите в папку `packages/common-rtc-s3` и запустите утилиту:
`np`

1. Пройдите шаги;
2. Сделайте пуш в репу новой версии.

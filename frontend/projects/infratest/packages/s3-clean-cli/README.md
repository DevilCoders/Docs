# s3-clean-cli

> CLI утилита для удаления expired-артефактов из MDS.

## Установка

```shell
npm install @yandex-int/si.ci.s3-clean-cli --registry=https://npm.yandex-team.ru
```

## Usage

```shell
s3-clean-cli.js <bucket>


Deletes all expired objects from specified S3 bucket.

Required ENV variables: "S3_ACCESS_KEY_ID", "S3_SECRET_ACCESS_KEY".


Options:
  --help, -h      Show help                                                       [boolean]
  --version, -v   Show version number                                             [boolean]
  --expires-from  A date (ISO8601) to validate expired objects (defaults to now)  [string]
  --endpoint      S3 host (s3.mdst.yandex.net by default)                         [string]
```

## Пример использования

```shell
S3_ACCESS_KEY_ID=your-key-id
S3_SECRET_ACCESS_KEY=your-access-key

npx @yandex-int/si.ci.s3-clean-cli test-bucket --expires-from=2019-01-16 --endpoint=s3.mds.yandex.net
```

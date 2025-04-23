# Dicts.Dumper

## Запустить
Пример для распового тестового бакета mds

- токен к sandbox [тут](https://sandbox.yandex-team.ru/oauth)
- получаем секреты к mds (например [секрет](https://yav.yandex-team.ru/secret/sec-01cmw91jcrtk5fpvjq0ev9wdnx/explore/versions))
```shell
cp templates/config.yaml config.yaml
vim config.yaml

ya make
./sandbox_to_s3_dicts_dumper
```

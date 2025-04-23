# yt-exporters

Обвязка для экспорта данных из couch/mysql/cassandra/etc в YT

[Документация](https://wiki.yandex-team.ru/vertis-admin/storage/perelivka-v-yt)

# Тестовый набор данных

Для нужд тесторования сделали тестовый набор данных из, это 10000 строк из:
инстанс: vertis
база: passport_autoru
таблица: user_moderation_status
Он находится в s3 - https://s3.mds.yandex.net/vertis-backups/prod/mysql/snapshots/test-instance.tgz.aes

Для тестирования с этим набором данных собран образ с protoc-файлом для аннотации поля data.
```
registry.yandex.net/vertis/test-instance-passport_autoru-user_moderation_status:latest
```

Запускать так:
```
docker run -e BACK_CRYPT_PASS=pass -e YT_TOKEN=token registry.yandex.net/vertis/test-instance-passport_autoru-user_moderation_status:latest test-instance passport_autoru user_moderation_status
```

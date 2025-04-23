# CheckMtdata

Задача для проверки корректности диффа (или полного состояния) [mtdata](https://a.yandex-team.ru/arc/trunk/arcadia/dict/mt/data.yaml)

Выполняет следующие проверки:
* Владельца ресурса (должен быть MT)
* Наличие бесконечного TTL на всех сендбоксовых ресурсах
* Наличие аттрибута creation_date

Опции:
* new_revision_hash - хэш новой ревизии, из которой возьмется содержимое data.yaml;
* old_revision_hash (опционально) - хэш старой ревизии, с которой будет сравниваться новая версия data.yaml;
* pull_request_id (опционально) - идентификатор PR в который в случае наличия ошибок будет добавлен комментарий с их списком;
* secret - идентификатор секрета в [YAV](https://yav.yandex-team.ru/), содержащий ключи arc-token и arcanum-token (опционально, нужно если указан pull_request_id)
* fix - пытаться исправить ошибки автоматически если это возможно

У задачи два режима работы:
* При передаче только new_revision_hash проверяется полное содержимое файла `dict/mt/data.yaml`
* При передаче old_revision_hash и new_revision_hash проверяется только дифф в этом файле

Пример запуска для отладки:
```
./check_mtdata run -o MT --type CHECK_MTDATA '{"custom_fields": [{"name":"new_revision_hash", "value":"4132136f4f5120156d0952f30ff64c6227df245c"}, {"name":"pull_request_id", "value": 2019831}, {"name":"secret", "value": "sec-01dws6hkyab1sn1mx6b7e7m7pg"}]}'
```

# Вычисление хэша по урлу документа

Rty не хранит полные урлы документов, вместо этого он использует md5 хэши этих урлов.
Эта тулза позволяет подобные хэши вычислить в нужном формате.

## Пример использования
Вычисляем хэш:
```
./rty_url_to_hash delivery_bucket_138778
9F537E5A5FE2052BE68AD5EC2CA02337
```

Проверяем наличие документа в сегменте RTY индекса на репорте:
```
root@sas2-5319-1f0-sas-market-test-rep-479-17050:/place/ssd/db/iss3/instances/17050_test_report_blue_sas_QUpxs3S3sVI# bin/tools/dump_ddk --segment-path data/search/rty_index/index_0000000000_0000004989/ | grep 9F537E5A5FE2052BE68AD5EC2CA02337
NOTICE: 2020-04-30 07:56:05.675 +0300 manager.cpp:6 Manager for DDK component opening...
NOTICE: 2020-04-30 07:56:05.675 +0300 manager.cpp:6 Manager for DDK component opening...
INFO: 2020-04-30 07:56:05.675 +0300 erf_disk.cpp:234 OPENING MANAGER: 0/data/search/rty_index/index_0000000000_0000004989/indexddk.rty/0
INFO: 2020-04-30 07:56:05.676 +0300 erf_disk.cpp:246 File is opening in read-only mode: data/search/rty_index/index_0000000000_0000004989/indexddk.rty
NOTICE: 2020-04-30 07:56:05.676 +0300 manager.cpp:12 Manager for DDK component opened OK
NOTICE: 2020-04-30 07:56:05.676 +0300 manager.cpp:12 Manager for DDK component opened OK
201    171190342    0    1588220525    9F537E5A5FE2052BE68AD5EC2CA02337    0    4250911257    256
NOTICE: 2020-04-30 07:56:05.835 +0300 manager.cpp:17 Manager for DDK component closing...
NOTICE: 2020-04-30 07:56:05.835 +0300 manager.cpp:17 Manager for DDK component closing...
NOTICE: 2020-04-30 07:56:05.835 +0300 manager.cpp:23 Manager for DDK component closed OK
NOTICE: 2020-04-30 07:56:05.835 +0300 manager.cpp:23 Manager for DDK component closed OK
NOTICE: 2020-04-30 07:56:05.835 +0300 manager.cpp:17 Manager for DDK component closing...
NOTICE: 2020-04-30 07:56:05.835 +0300 manager.cpp:23 Manager for DDK component closed OK
```

## Ссылки
- [dump_ddk](https://a.yandex-team.ru/arc/trunk/arcadia/saas/tools/dump_ddk)

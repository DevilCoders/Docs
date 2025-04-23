Для запуска надо проэкспортировать tvm токен (https://yav.yandex-team.ru/secret/sec-01erytvw6xtntdt3v38675awqn/explore/version/ver-01erytvw7w80gw60y3gn5nzv6x) и ключ метрики для расшифрования (https://yav.yandex-team.ru/secret/sec-01csvzeyhdgwmk5dq5bsntedh6/explore/versions):
```
./bin/socket_filter --filter 44.*
Reading: sas.logbroker.yandex.net/rtmr--crypta-rtdi-log by crypta-rtdi-test. Locked sessions: 0
timestamp: 1605533801, yandexuid: 4446503291601740568, android_id: "381ffc4eda249cbb", device_id: "69fb05d4262492e45e7ed2495914f629", uuid: "77a2b62224f1f74fe0e05e3e1c3cfef7", google_aid: "fdc11c9d-95a4-4627-bf13-c1e0a6ca8a07"
timestamp: 1605533801, yandexuid: 4446503291601740568, android_id: "381ffc4eda249cbb", device_id: "69fb05d4262492e45e7ed2495914f629", uuid: "77a2b62224f1f74fe0e05e3e1c3cfef7", google_aid: "fdc11c9d-95a4-4627-bf13-c1e0a6ca8a07"
timestamp: 1605533801, yandexuid: 4461676941598353137, device_id: "ddc2c1c052b1830d869e199a4a5228f2", uuid: "5ab4a93166522c9b33c228713d2f6093", google_aid: "9a198165-e605-4eb5-8787-a558e2d24113"
timestamp: 1605533801, yandexuid: 4461676941598353137, device_id: "ddc2c1c052b1830d869e199a4a5228f2", uuid: "5ab4a93166522c9b33c228713d2f6093", google_aid: "9a198165-e605-4eb5-8787-a558e2d24113"
timestamp: 1605533801, yandexuid: 4461676941598353137, device_id: "ddc2c1c052b1830d869e199a4a5228f2", uuid: "5ab4a93166522c9b33c228713d2f6093", google_aid: "9a198165-e605-4eb5-8787-a558e2d24113"
timestamp: 1605533796, yandexuid: 4435331791591718097, device_id: "ab2e0cb92a5e95d93433931982cb5973", huawei_aid: "ffdc1bbd-ddbf-ff7c-ebff-bff77cf93936", uuid: "6f215c32a1b7835f6513c97c76e13363", google_aid: "a3997512-0e8e-4009-91a6-68b6a5c84249"
```

Печатаются все мессаджи, в которых хотя бы один идентификатор попал хотя бы под одну регулярку ```--filter```.

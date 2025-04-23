# ads.emily.storage.models.client

Клиенты для работы с хранилищем моделей.

## Разработка

- Запустить тесты

```bash
ads/emily/storage/models/client/mt$ ya make -rttt . --test-stderr
```

## Выгрузка из царя

### Тестовая выгрузка локально

- Цари - [https://sandbox.yandex-team.ru/resource/1963718680/view](https://sandbox.yandex-team.ru/resource/1963718680/view)

```bash
# Сделать конфг обработки
ads/pytorch/lib/online_learning/production/processors/tsar_processor$ cat model_processor_conf.json
[
    {
        "yt_model_name": "page",
        "local_model_name": "PageNamespaces_3",
        "sandbox_resource_type": "TORCH_TSAR_PAGE_MODEL",
        "transport_type": "TsarTransport"
    },
    {
        "yt_model_name": "page2",
        "local_model_name": "Page2Namespaces_3",
        "sandbox_resource_type": "TORCH_TSAR_PAGE_MODEL",
        "transport_type": "TsarTransport"
    }
]

# Закомментровать в коде [альтернативные выгрузки](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/lib/online_learning/production/processors/tsar_processor/lib/processing_impl.py?rev=r7938733#L139) (долго работает на данный момент)

# Собрать бинарь
ads/pytorch/lib/online_learning/production/processors/tsar_processor$ ya make -r .

# Запустить выгрузку
ads/pytorch/lib/online_learning/production/processors/tsar_processor$ YT_PROXY=hahn YT_TOKEN=<> SANDBOX_TOKEN=<> ./tsar_processor --direct_value_path //home/bs/users/ilariia/tsar_processed_model2/13 --transport http --model_descriptors_config ./model_processor_conf.json --ttl 500 --model_id 10 --model_yt_dir //home/fake_dir --artifact_name artname_ilariia --force
```

### Тестовая выгрузка на сандбоксе

```bash
# Собрать бинарь и пострипать
ads/pytorch/lib/online_learning/production/processors/tsar_processor$ ya make -r && strip tsar_processor

# Загрузить в ресурс
ads/pytorch/lib/online_learning/production/processors/tsar_processor$ ya upload tsar_processor -T TORCH_TSAR_PROCESSOR_BINARY -A test_runner=emily
```

Сделать Run Once в [шедулере](https://sandbox.yandex-team.ru/scheduler/44088/view) (это копия продового [шедулера](https://sandbox.yandex-team.ru/scheduler/43663/view) c измененными параметрами)

### Продовая выгрузка на сандбоксе

- Пересобрать ресурс `TORCH_TSAR_PROCESSOR_BINARY`, скопировав [последний таск](https://sandbox.yandex-team.ru/resources?type=TORCH_TSAR_PROCESSOR_BINARY), указав ревью в дескрипшене и ревизию сборки
- Попросить владельцев ресурса нажать кнопку `release`
- Проверить, что все ок в [шедулере](https://sandbox.yandex-team.ru/scheduler/43663/view)

## Обновить бинарь

### Сборка и релизы

Stable релизы подхватываются Нирваной автоматически.

#### Ресурсы

- Клиент [ML_STORAGE_CLI_BINARY](https://sandbox.yandex-team.ru/resources?type=ML_STORAGE_CLI_BINARY&limit=20)
- ML Engine препроцессор [ML_STORAGE_PREPROCESSOR_ML_ENGINE_BINARY](https://sandbox.yandex-team.ru/resources?type=ML_STORAGE_PREPROCESSOR_ML_ENGINE_BINARY&limit=20)

Ресурсы автоматически собираются в CI

## Nirvana

### Обновить операцию

[readme](https://a.yandex-team.ru/arc/trunk/arcadia/ads/emily/storage/libs/nirvana/readme.md)

### Протестировать

#### ML Engine

- Получить [ML Engine OAuth Token](https://oauth.yandex-team.ru//authorize?response_type=token&client_id=37053ffeeb0b4099bafd84242d5850a5)
- Добавить в [sandbox vault](https://sandbox.yandex-team.ru/admin/vault), [секретницу](https://yav.yandex-team.ru/) и [пролинковать с nirvana](https://nirvana.yandex-team.ru/secrets)

```bash
# Собрать тулзу
cd ads/ml_engine/tool && ya make -r


# Linear Model
# Поменять овнера, название модели и почту для уведомлений
# yabs/utils/learn-tasks2/ml-storage/tlm/vw_llp_ctrs_small.yml

./ml_engine ~/arc/arcadia/yabs/utils/learn-tasks2/ml-storage/tlm/vw_llp_ctrs_small.yml --nirvana-secret <ml_engine_secret_name>

# Matrixnet
# days = 1, common_prefix = ml_storage_test, mail_to = <your mail>, last_log_date = <actual date>
# yabs/utils/learn-tasks2/ml-storage/mx/F19_baseline/F19_prod_abuse_fresh_rc_from_log_fixes_4_09_pytorch_new_tsar.yml
./ml_engine ~/arc/arcadia/yabs/utils/learn-tasks2/ml-storage/mx/F19_baseline/F19_prod_abuse_fresh_rc_from_log_fixes_4_09_pytorch_new_tsar.yml  --nirvana-secret <ml_engine_secret_name>
```

**Что получится:**

**Linear Model**

- [Nirvana Graph](https://nirvana.yandex-team.ru/flow/26d488b1-5b17-4f7e-9e86-4776dc64ed08/f42084ed-28e6-4de7-b2bc-d1cacb75cd7c/graph)
- [Ресурс](https://sandbox.yandex-team.ru/resource/2047105013/view)

**Matrixnet**

- [Nirvana Graph 1](https://nirvana.yandex-team.ru/flow/4d2159bb-a6b1-4852-85f7-8c879ce8bd98/099e2d81-7791-46c1-8b47-e7fda4fee336/graph)
- [Nirvana Graph 2](https://nirvana.yandex-team.ru/flow/b0e5537f-b423-4d47-bb54-2ed3d412223a/ed91aebc-cb1b-40d8-9c5c-a11b47c04e0a/graph)

#### Bid Correction

```bash
# Собрать тулзу
cd ads/quality/bid_correction/workflow_constructor && ya make -r

./workflow_constructor --mode lm_prod --lm_tasks ~/arc/arcadia/ads/quality/bid_correction/workflow_constructor/tasks/ab_conv/rsya/lm/v10_dmlc_rwm1_roi.yml --tmp_tables_ttl 1 --nirvana_results_ttl 1 --last_log_date 20210301 --lm_tasks_patch '{"days": 1}' --no_start

# Граф создастся, запускать вручную (предварительно выставив nirvana-secret, можно использовать ML_ENGINE)
```

**Что получится:**

- [Nirvana Graph](https://nirvana.yandex-team.ru/flow/e6d23498-cba0-4dd4-916d-f00ae1906c9e/714a1b12-a3f5-46f8-8156-57df56f41ba2/graph)
- [Ресурс](https://sandbox.yandex-team.ru/resource/2048900552/view)

## Eagle

[Конфиг модели](https://a.yandex-team.ru/arc_vcs/ads/bsyeti/samogon/eagle/plugin/eagle.py?rev=6ce2e23375ac2d8dba6e39c706b4a1fff898dd90#L168)
[Конфиг ресурсов](https://a.yandex-team.ru/arc_vcs/ads/bsyeti/samogon/plugin_lib/sandbox_resources/sandbox_resources_set.py?rev=ca77413401d99f4346750328c93a19ef614dd44a#L154)

```bash
# Деплой на 10 стенд Eagle
ads/bsyeti/samogon/eagle/deploy.sh 10
```

Деплой логи: https://dl-deploy.n.yandex-team.ru/dynamic/dleagle10
Логи стенда: https://bootstrapeagle1011man-monproxy-eagle10.n.yandex-team.ru/servants/user/
Дашборд: https://solomon.yandex-team.ru/?cluster=eagle_10&project=eagle&service=eagle_10&dashboard=eagle_load&l.host=cluster&l.servant=eagle&b=1h30m

### Релизы

#### ML Engine Regular Task

- [Инструкция](https://wiki.yandex-team.ru/users/ohmikey/updatebinarysandboxlogcreator/)
- Зарелизить [YA_MAKE](https://sandbox.yandex-team.ru/task/887837551/view)

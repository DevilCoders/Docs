# Тасклеты для поиска и ожидания появления требуемых ресурсов

## Обновление

### Доступные тасклеты

```sh
make list
```

### Обновление тасклетов

```sh
make upload
```

В терминале будет id нового ресурса и ссылка на mds таску с загрузкой этого ресурса.

```sh
2021-07-15 13:34:41.688 INFO   MainThread (tasklet/domain/sandbox/utils.py:24) Uploading tasks resource to Sandbox
2021-07-15 13:34:42.365 INFO   MainThread (sandbox/taskbox/binary/__init__.py:235) 1 file (86.07MiB) to upload
2021-07-15 13:34:43.130 INFO   MainThread (sandbox/taskbox/binary/__init__.py:248) Uploading task #1019372660 created: https://sandbox.yandex-team.ru/task/1019372660
2021-07-15 13:34:56.333 INFO   MainThread (sandbox/taskbox/binary/__init__.py:257) Resource is in READY state
2021-07-15 13:34:56.618 INFO   MainThread (tasklet/domain/sandbox/utils.py:53) Tasks resource has uploaded: https://sandbox.yandex-team.ru/resource/2285864521
2285864521
```

заменяем `id` в файле тасклета

- [ci/registry/projects/logos/wait_for_resource.yaml](../../../../../../ci/registry/projects/logos/wait_for_resource.yaml)

и коммитим. Если всё работает, релизим ресурс, нажав на кнопку релиза в mds таске, **иначе бинарь удалится через 14 дней.**

## Отладка

### WaitForResource

Тасклет для загрузки Валидационного конфига индексера с проставлением версии конфига в аттрибутах.

Посмотреть схему таска:

```sh
make schema
```

Запуск тасклета на сендбоксе

```sh
make run-sandbox
```

перед запуском убедитесь, что в Sandbox Vault у вас есть токен c именем [glycine_oauth_token](https://docs.yandex-team.ru/ci/quick-start-guide#get-glycine-token)

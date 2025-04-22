# Тасклет для проверки моделей в сторадже

[Документация](https://logos.yandex-team.ru/docs/ml_logos/storage/development/tests#check-storage-diff)

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

- [ci/registry/projects/logos/check_storage_diff.yaml](../../../../../../ci/registry/projects/logos/check_storage_diff.yaml)

и коммитим. Если всё работает, релизим ресурс, нажав на кнопку релиза в mds таске, **иначе бинарь удалится через 14 дней.**

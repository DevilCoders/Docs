# RunInventoriYqlTask

## Общий принцип как это работает:

- Так как это python3 таска, то она запускается только в режиме --enable-taskbox
  Это означает, что и server-side методы (on_save, on_create, on_enqueue)
  запускаются из бинаря. Потому можно делать импорт не sandbox проектов на уровне модуля.

- При сохранении таски берется последний зарелиженый stable ресурс,
  если это указано в параметре binary_executor_release_type
  (логика прописана в LastBinaryTaskRelease)
  Так что не стоит обращать внимание на то, какой бинарник прописан в шедулере
  или на основе какого вы создавали таску/шедулер в UI Sandbox'а (см. далее)

- К сожалению по дефолту этот тип ресурса не будет виден в UI Sandbox'а
  Надо выбрать бинарь, чтобы появилась такая возможность. Нулевой - 2425391032
  В созданой таске/шедулере выбрать binary_executor_release_type=stable

## Для релиза:

Для сборки можно использовать [DEPLOY_BINARY_TASK](https://sandbox.yandex-team.ru/task/1200668286/view)
Важные параметры:
* Arcadia URL (arcadia_url) - версия кода которую собрать (по умолчанию `arcadia-arc:/#trunk`)
* Binary task archive attributes (attrs) - атрибут task_type: RUN_INVENTORI_TASKS
  по которому будет определяться что ресурс является бинарным кодом RUN_INVENTORI_TASKS
* Check these task types are present in result program (check_types) -
  проверка что соответствующий тип есть в бинаре RUN_INVENTORI_TASKS
* Yav secret with OAuth token for Arc (arc_oauth_token) - `sec-01eb89vakhn60j7ynwmr16a9ne#arc-token`
* Vault YT token vault entry (yt_token_vault) - токен для кеширование с помощью YT
  (вроде как ускоряет сборку) INVENTORI_YT_TOKEN

Так же возможен ручной вариант сбоки.

Следующей командой забилдить и запустить таску.
```
ya make && ./run-inventori-yql-task run --type RUN_INVENTORI_YQL_TASK \
  --attr task_type=RUN_INVENTORI_YQL_TASK --enable-taskbox  --create-only \
  '{"custom_fields": [ {"name": "binary_executor_release_type", "value": "custom"}]}'
```

По типу таски `--attr task_type=...` будет определяться подходящий для запуска бинарник
при binary_executor_release_type=stable или testing etc.
Однако по дефолту выставлено значяение custom,
так что при запуске он не будет подменяться на свежий.
Таким образом можно этот ресурс протестировать,
затем перейти к таске, которой он создан, и зарелизить ее.

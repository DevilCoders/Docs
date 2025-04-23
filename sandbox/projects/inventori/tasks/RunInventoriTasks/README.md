# RunInventoriTasks

Раннер - таска для запуска/шедулинга "продуктовых" бинарей.

Добавление и управление параметрами раннера осуществляется в [common/resources.py](https://a.yandex-team.ru/arcadia/sandbox/projects/inventori/common/resources.py)
путем добавления класса параметров таски с декоратором register_inventori_task:

```python
@register_inventori_task(
    name='task_name',
    path_to_task_class='inventori.pylibs.tasks.task_name.Task',  # nested from inventori.pylibs.tasks.base.BaseTask
)
class InventoriTaskParams(InventoriBaseTaskParams):
    some_param = parameters.StrParam('Some param')


```

Чтобы новые параметры проросли в UI SandBox'а надо либо закоммитить их в транк,
либо создавать шедулер с указанием бинарного ресерса собранного с данным изменением.

Пересобрать раннер можно с помощью таски [DEPLOY_BINARY_TASK](https://sandbox.yandex-team.ru/task/1186565032)
с указанием следующих параметров (для удобства можно просто склонировать от успешной сборки):

* Arcadia URL (arcadia_url) - версия кода которую собрать (по умолчанию `arcadia-arc:/#trunk`)
* Binary task archive attributes (attrs) - атрибут task_type: `RUN_INVENTORI_TASKS`
  по которому будет определяться что ресурс является бинарным кодом RUN_INVENTORI_TASKS.
  Можно так же собрать с атрибутом task_type: `RUN_INVENTORI_TASKS:task_name` - тогда после релиза,
  собранный ресурс будет применен только для тасок соответствующего типа.
* Check these task types are present in result program (check_types) -
  проверка что соответствующий тип есть в бинаре RUN_INVENTORI_TASKS
* Yav secret with OAuth token for Arc (arc_oauth_token) - `sec-01eb89vakhn60j7ynwmr16a9ne#arc-token`
* Vault YT token vault entry (yt_token_vault) - токен для кеширование с помощью YT
  (вроде как ускоряет сборку) INVENTORI_YT_TOKEN

Сборку можно зарелизить как tesing тогда данная версия будет браться
только при запуске [тестовых шедулеров](https://sandbox.yandex-team.ru/schedulers?owner=INVENTORI&tags=TEST&task_type=RUN_INVENTORI_TASKS&limit=100)
(так как в них мы проставляем параметр Release type of binary executor resource(binary_executor_release_type): testing_or_upper),
или как stable - тогда будет браться и для [продовых шедулеров](https://sandbox.yandex-team.ru/schedulers?owner=INVENTORI&tags=PROD&task_type=RUN_INVENTORI_TASKS&limit=100)
(соответственно параметр Release type of binary executor resource(binary_executor_release_type): stable).

Для отладки можно создать таску/шедулер c параметром Release type of binary executor resource(binary_executor_release_type): custom
и в параметр Advanced -> Task resource прописать id собранного ресурса.

## Local build

To locally build this Sandbox task use next command from `/bin` folder.

### Simple build

```bash
ya make && ./run-inventori-tasks run --type RUN_INVENTORI_TASKS --enable-taskbox --create-only --owner INVENTORI \
  '{"custom_fields": [ {"name": "binary_executor_release_type", "value": "custom"}]}'
```

### Advanced build version.

Build version with specific product task – daily_pi_data_collector. !It must be already built, because here we use id: "2719734053" for custom mode.

```bash
ya make && ./run-inventori-tasks run --type RUN_INVENTORI_TASKS --enable-taskbox --create-only \
'{"custom_fields": [ {"name": "binary_executor_release_type", "value": "custom"},
{"name": "_task_type", "value": "INVENTORI_DAILY_PI_DATA_BINARY"},
{"name": "daily_pi_data_collector_executable", "value": "2719734053"},
{"name": "daily_pi_data_collector_result_folder", "value": "//home/inventori/alekseyen/daily_pi_data"},
{"name": "solomon_token", "value": ""}, {"name": "dup_type", "value": "async"}], "description": "Test alekseyen run"}' --owner INVENTORI
```
Your output from command above:
```
2022-02-07 15:42:37 INFO 1 file (409.93MiB) to upload
2022-02-07 15:42:37 INFO Uploading task #1207728446 created: https://sandbox.yandex-team.ru/task/1207728446
2022-02-07 15:44:15 INFO Resource is in READY state
2022-02-07 15:44:32 INFO Task of type RUN_INVENTORI_TASKS created: https://sandbox.yandex-team.ru/task/1207730363
{"resource": {"id": 2767027394, "type": "SANDBOX_TASKS_BINARY", "task": {"status": "WAIT_RES", "url": "https://sandbox.yandex-team.ru/api/v1.0/task/1207728446", "id": 1207728446}, "attributes": {"binary_age": "7", "commit_revision": "9066027", "taskbox_enabled": "True", "backup_task": true, "binary_hash": "9bfe8bcf6708af279e8c1fd6aae79c46"}}, "task": {"id": 1207730363, "type": "RUN_INVENTORI_TASKS", "owner": "INVENTORI"}}
```
So, copy second link in browser and play (from example above https://sandbox.yandex-team.ru/task/1207730363)


Also u can delete binary_executor_release_type = custom and use trunk(stable) version, so u don't need to specify id of your executable type

# BuildInventoriTasks
Таска для сборки "продуктового" бинаря, который можно будет запускать через [RUN_INVENTORI_TASKS](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/inventori/tasks/RunInventoriTasks) указав id собранного ресурса в параметре Task executable.

Так как API SandBox'а для работы с ресуроми необходимо, чтобы их описание (описание класса наследуемого от sdk2.Resource) было в trunk'е аркадии и доступно по PEERDIR из /sandbox/projects (см. [документацию](https://docs.yandex-team.ru/sandbox/dev/resources#new-type)) ресурса надо закоммитить в **tunk** его описание с параметром arcadia_build_path (путь до target'а) и декоратором `@register_as_inventori_task`. После этого (после коммита надо подождать минут 10) можно создать таску с типом BUILD_INVENTORI_TASKS где появится в качестве варианта выбора нового "продуктового" бинаря.

## Сборка
Для ручной сборки использовать:
```bash
ya make && ./build-inventori-tasks run --type BUILD_INVENTORI_TASKS --attr task_type=BUILD_INVENTORI_TASKS --enable-taskbox  --create-only \
'{"custom_fields": [ {"name": "binary_executor_release_type", "value": "custom"}], "description": "Test alekseyen run"}' --owner INVENTORI
```

(А не для ручной, использовать общую таску SB таску DEPLOY_BINARY_TASKS, аналогично с раннерами)

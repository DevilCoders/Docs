## Таски для CI ClickHouse

### Тестирование изменений в тасках
Данные таски поддерживают бинарную сборку, но пока не переключены на использование бинарной сборки по умолчанию.
Что это значит — можно проверить изменения в CI тасках без мерджа в trunk.

Для релиза(использования нового кода по умолчанию) рекомендуется в любом случае сделать коммит в trunk.
Для бинарных тасков настроен автоматический релиз описанного ниже ресурса при коммите в `sandbox/projects/clickhouse` и его зависимости.
Возможен, но не рекомендуется по умолчанию, вариант ручного обновления ресурса, который будет использоваться в sandbox в обход сборки через TestEnv.

1) Как проверить linter:
```bash
ya make -A
```
В папке конкретного таска или в `sandbox/projects/clickhouse`, где лежит данный readme.

2) Как проверить таск:

* Собрать код. Для этого достаточно результат работы `ya make -A` в папке `sandbox/projects/clickhouse` или `sandbox/projects/clickhouse`.
Для релиза в продакшен данного ресурса лучше использовать ключ `-r`/`--build=release`.
После сборки в папке bin лежит бинарник `clickhouse-sb-runner`.
Это специальная обертка над sandbox тасками, которая умеет загружать ресурс(себя) в sandbox и запускать таски из консоли.
* Сначала можем проверить, что в нем есть код вашего таска, если он новый:
```bash
clickhouse-sb-runner content --list-types. В выдаче должны увидеть название вашего таска
```
В списке тасков должно быть название вашего таска. Если его нет, проверьте, что добавили его в PEERDIR и пересобрали бинарник.
* Чтобы запустить таск с локально собранной версией:
на примере таска `CLICKHOUSE_PULL_REQUEST_PATCHER`.
```bash
./clickhouse-sb-runner run -v -o CLICKHOUSE --type CLICKHOUSE_PULL_REQUEST_PATCHER '{"custom_fields": [{ "name":"commit_sha", "value": "fea24d0f98261c121d1afa7d80cdc65fe42c89a3"}, {"name": "pull_request_number",  "value": 0}, {"name": "binary_executor_release_type",  "value": "custom"}]}'
```
В JSON поле `custom_fields` лежит словарик с параметрами.
Указывать дефолтные параметры не требуется.
* Альтернативный способ запуска, чтобы не писать JSON как в предыдущем пункте, можно просто предсоздать таск и изменить настройки уже в интерфейсе:
```bash
./clickhouse-sb-runner run -v -o CLICKHOUSE --type CLICKHOUSE_UNIT_TEST --create-only
```

Еще один вариант, как воспольоваться собранным ресусом при запуске.
Загрузить ресурс в Sanbdox:
```bash
./clickhouse-sb-runner upload -o CLICKHOUSE --attr task_type=CLICKHOUSE_SANDBOX_BINARY --attr released=testing  --skynet
```
На странице запуска таска выбрать `binary_executor_release_type=testing`. Самый свежий ресурс выберется автоматом. То есть после клонирования существующей таски достаточно поменять одно поле чтобы сравнить два запсука с общими параметрами.
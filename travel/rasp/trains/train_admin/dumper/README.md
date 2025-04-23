## dumper
Приложение, отвечающее за выгрузку данных из базы Поездов в .pb2 файлы.
Используется в sandbox задаче [DumpTrainData](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/rasp/DumpTrainData).

### Добавление новых протобаф ресурсов
1. Добавить новый прото ресурс в папку [trains](https://a.yandex-team.ru/arc/trunk/arcadia/travel/proto/dicts/trains),
либо скопировать существующий из папки расписаний [rasp](https://a.yandex-team.ru/arc/trunk/arcadia/travel/proto/dicts/rasp).
2. Создать соответствующую Django модель, например [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/trains/train_admin/train_admin/models.py).
3. Написать класс в папке `dumpers`, смапив модель с протобаф ресурсом по аналогии с существующими.
4. Добавить использование класса в основной дампер `dumper.py`, указав файл выгрузки данных.
5. Обновить дампер в Sandbox:
```shell script
ya package dumper/package.json --raw-package --upload --upload-resource-type=DUMP_TRAIN_DATA_RESOURCE --upload-resource-attr=resource_name=dumper
```
6. Запустить Sandbox задачу `DumpTrainData`.

### Использование новых прото ресурсов в train_api
В train_api использование прото ресурсов происходит под динамической настройкой [TRAIN_BACKEND_USE_PROTOBUFS](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/library/python/common/apps/train_order/__init__.py#L139).
При создании и использовании новых прото ресурсов необходимо добавить новый ключ в указанную настройку.

### Как найти созданные ресурсы
Ресурсы типа DUMP_TRAIN_DATA_RESOURCE, нужные ищем по аттрибуту `resource_name`.

[Ссылка на Sandbox](https://sandbox.yandex-team.ru/resources?type=DUMP_TRAIN_DATA_RESOURCE)

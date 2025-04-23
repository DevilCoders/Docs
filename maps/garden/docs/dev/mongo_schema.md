# Структура базы данных Огорода

## Билды

### builds

Коллекция хранит информацию обо всех текущих неудалённых билдах:

* имя модуля, версию модуля, номер билда
* автора (кто запустил билд)
* свойства билда (shipping_date, release_name, region, vendor, autostarted)
* список источников (источником может быть другой билд или ресурс)
* список созданных ресурсов (ключ указывает на ресурс в таблице **resources**)
* текущий статус (шедьюлится, выполняется, завершён и т.д.)

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/build/builds_storage.py#L10)

### requests

В ядре Огорода запущенному билду соответствует понятие "запроса". Запросы обслуживает класс `RequestHandler`. Этот класс выполняет шедьюлинг, посылает задачи в `TaskHandler` по мере удовлетворения `demands`.

Информация о запросах хранится в коллекции **requests** и обновляется по ходу выполнения запроса:

* сколько всего тасок должно быть запущено
* сколько тасок завершилось успешно и сколько неуспешно (и тексты ошибок)
* какие ресурсы должны быть созданы (имена, ключи, хэши)

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/graph/request_storage.py#L186)

{% note warning %}

Судя по коду и по размеру коллекции, старые запросы не всегда удаляются из базы даных. Необходимо найти и устранить утечку.

{% endnote %}

### build_statistics

Коллекция хранит информацию обо всех билдах за всё время. Записи не удаляются из этой коллекции.

По сравнению с коллекцией **builds**:

* отсутствует список созданных ресурсов
* есть список запросов из коллекции **requests** (каждый рестарт билда порождает новый запрос)

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/build/build_statistics.py#L154)

### build_actions

Запросы на создание билда и на изменение статуса билда: удаление, отмена, рестарт и т.д.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/build/build_actions.py#L12)

### actual_sources

Коллекция хранит информацию об актуальных датасетах для билдов **source** модулей, которые были созданы через механизм сканирования ресурсов.
Информация о датасетах общая для всех контуров. Информация о датасетах для билдов созданных через post не хранится в этой таблице (если только эти же датасеты не присылает сканер ресурсов).
Уникальность датасета определяется по **foreign_key**. В одном контуре может быть только один билд конкретного **source** модуля от одного датасета.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/build/source_build_registrar.py#L30)

## Модули

### module_versions

Коллекция содержит информацию о версиях модулей.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/module/module_manager.py#L53).

### settings

Коллекция содержит настройки модулей, которые можно изменять в рантайме.

В настоящий момент для каждого модуля хранится группа настроек **autostart**.
Автостарт считается включенным по умолчанию, поэтому наличие элемента в коллекции **говорит об отключенном автостарте**.

Автостарт отключается запросом `POST /modules/<module_name>/disable-autostart/`,
включается обратно запросом `POST /modules/<module_name>/enable-autostart/`.

Содержимое коллекции можно запрашивать через `GET /modules/<module_name>/`.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/module/module_settings_storage.py#L17)

### module_events

События с модулями: операции над билдами, операции над версиями модулей, включение и выключение автостарта.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/log_storage/module_event_storage.py#L38)

### module_logs

Логи модулей: автостартер, автоудалятор, сканирование ресурсов.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/log_storage/module_log_storage.py#L27)

## Ресурсы

### resources

Коллекция хранит ресурсы Огорода. Ресурс добавляется в коллекцию после успешного завершения задачи, которая его создаёт. Ресурс удаляется при удалении билда.

Из-за ошибок при удалении возможна утечка ресурсов.
Есть два вида утечек:
* В таблице хранится информация о ресурсах, которых нет во внешних хранилищах
* В таблице нет информации о ресурсах, которые есть во внешних хранилищах

Первый вид утечек не мониторится. Что произойдёт с таким ресурсом при попытке его удаления зависит от типа ресурса.

Для устранения второго вида утечек есть инструмент */garden/tools/unaccounted_resources*. Подробнее о том как его использовать написано в [readme](https://a.yandex-team.ru/arc_vcs/maps/garden/tools/unaccounted_resources/readme.md).

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/resource_storage/storage.py#L31)

### deferred_removal_resources

При удалении билда ресурсы, у которых свойство `allow_deferred_removal=True`, не удаляются сразу,
а помещаются в эту коллекцию. Отдельный фоновый процесс с заданной периодичностью просматривает коллекцию и пытается удалить ресурсы. Если ресурс не удаётся удалить за несколько попыток, то он помечается как `obsolete`.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/resource_storage/deferred_removal.py#L98)

### dangling_resources

Если у ресурса свойство `allow_deferred_removal=False`, и его не удалось удалить с первого раза, то ресурс помещается в эту коллекцию.
Впоследствии отдельный процесс шедьюлера пытается удалять ресурсы попавшие в эту коллекцию. Если, в течении определённого количества попыток или времени, удалить не удаётся, то поджигается мониторинг **dangling_resources**.
Также в таблице хранится информация об ошибке произошедшей при попытке удаления.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/resource_storage/dangling_resource_manager.py#L45)

### resource_statistics

Информация о созданных ресурсах для показа на странице билда (Perf). Информация остаётся в коллекции даже при удалении ресурса. TTL 3 месяца.
Данные в таблицу пишет тул [perf_normalizer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/tools/perf_normalizer)

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/task/task_log_manager.py#L408)

## Задачи (Tasks)

### task_monitor

Коллекция хранит информацию о текущих зашедьюленных и запущенных тасках для показа на странице Task Monitor.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/common/task_monitor_storage.py#L42)

### tasks

Входные и выходные данные тасок - используется в джобах в YT.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/task/task_storage.py#L74)

### task_log

Сюда пишется информация о том, в какой ванилла-операции запустилась таска, с какими ресурсами и когда завершилась.
Процесс `perf_normalizer` перерабатывает записи из этой коллекции и перекладывает в коллекции `tasks_statistics` и `resource_statistics`.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/task/task_log_manager.py#L330)

### task_statistics

Информация о тасках, которые запускались и завершились в Огороде. Используется для показа на странице билда (Perf). TTL 3 месяца.
Данные в таблицу пишет тул [perf_normalizer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/tools/perf_normalizer)

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/task/task_log_manager.py#L366)

### task_operations

Ванилла и MR-операции, которые запускались тасками. Используется для показа на странице билда (Perf). TTL 3 месяца.
Данные в таблицу пишет тул [operation_fetcher](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/tools/operation_fetcher)

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/task/operation_storage.py#L210)

## Прочее

### contours

Коллекция содержит информацию о контурах:
* имя контура
* кто владелец модуля
* признак: является ли контур системным

Для пользовательских контуров хранятся активные версии модулей.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/common/contour_manager.py#L37)

### autostart_requests

Запросы на автостарт модулей.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/autostart/subprocess_autostart_manager.py#L73)

### scan_resources_requests

Запросы на сканирование ресурсов

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/module/scan_resources_common.py#L22)

### acl

Права доступа к модулям и используется в связке с IDM.

[Код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/acl_manager/acl_manager.py#L26)

### parameters

Набор пар ключ-значение для обмена данными между шедьюлером Огорода и тулами.

### counters

Коллекция содержит счётчики. Каждая запись представляет один счётчик и содержит 2 поля: имя счётчика (`_id`) и значение счётчика.

Для каждого модуля есть свой счётчик, который хранит номер последнего билда этого модуля.

Используется в 2х местах:

* [BuildManager](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/build/build_manager.py#L20)
* [MongoRequestStorage](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs_server/graph/request_storage.py#L186)

### schema_version

Коллекция содержит единственную запись с номером последней накаченной миграции.
При запуске сервера миграции накатываются в функции [run_migration](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/server/migration/migrate_database.py?rev=5096278#L197).

# Как писать юнит-тесты для огородных модулей

Могут быть 3 уровня тестов:

* Тесты графа тасок (функции `fill_graph`)
* Тесты отдельных тасок в составе модуля
* Тесты всего модуля целиком

Все бинарные модули в обязательном порядке должны иметь тест графа тасок.
Крайне рекомендуется иметь тесты для тасок или всего модуля.

## Тесты графа тасок

Делается методом copy-paste.

```python
from maps.garden.libs import test_utils
from maps.garden.modules.mymodule.lib import mymodule


def test_fill_graph():
    test_utils.graph.validate_fill_graph_routine(mymodule.fill_graph)
```

## Общие настройки

### ya.make

Если тест использует локальный YT, то в `ya.make` добавить:

```
IF(NOT ${DONT_BUILD_YT_YQL})
    INCLUDE(${ARCADIA_ROOT}/mapreduce/yt/python/yt_stuff.make.inc)
ENDIF()
```

Флаг `DONT_BUILD_YT_YQL` используется для ускорения запуска тестов, если есть заранее поднятый локальный YT. Пример:
```
CUSTOM_LOCAL_YT=localhost:<your port> ya make -A -DDONT_BUILD_YT_YQL
```

{% note warning %}

В Аркадии есть ещё один вариант поднять локальный YT - рецепт, который подключается через

```
INCLUDE(${ARCADIA_ROOT}/mapreduce/yt/python/recipe/recipe.inc)
```

Его использовать не рекомендуется, т.к. YT стартует безусловно для всех тестов,
даже если некоторым тестам не нужен YT.

{% endnote %}

Если тест использует локальные YT и YQL, то:

```
IF(NOT ${DONT_BUILD_YT_YQL})
    INCLUDE(${ARCADIA_ROOT}/yql/library/local/ya.make.19_4.inc)
ENDIF()
```

Флаг `DONT_BUILD_YT_YQL` используется для ускорения запуска тестов, если есть заранее поднятый локальный YT и YQL. Пример:
```
CUSTOM_LOCAL_YT=localhost:<YT port> CUSTOM_LOCAL_YQL=localhost:<YQL port> ya make -A -DDONT_BUILD_YT_YQL
```

Также если в YQL скриптах используются UDF-функции, то нужно прописать путь к ним в блоке `DEPENDS`, например:
```
DEPENDS(
    yql/udfs/common/datetime2
)
```

### Окружение

В библиотеке `maps/garden/libs/test_utils` определена фикстура `environment_settings`,
которая умеет поднимать нужное окружение для тестов:

```python
def test_something(environment_settings)
```

Чтобы подключить фикстуру, нужно поставить `PEERDIR` на эту библиотеку.
Поведение фикстуры регулируется маркерами, которые вешаются на тестовую функцию.

Чтобы поднять локальный YT:

```python
@pytest.mark.use_local_yt("hahn")
def test_something(environment_settings)
```

Чтобы поднять локальные YT и YQL:

```python
@pytest.mark.use_local_yt_yql
def test_something(environment_settings)
```

Локальные инстансы YT и YQL поднимаются один раз на каждый py-модуль.

Во время локальной отладки тестов можно ускорить запуск, если заранее поднять свой собственный
инстанс YT по инструкции https://yt.yandex-team.ru/docs/other/local_mode

Адрес своего инстанса YT нужно передавать в тесты через переменную окружения `CUSTOM_LOCAL_YT`. Пример:

```bash
CUSTOM_LOCAL_YT=wicket.sas.yp-c.yandex.net:8010 ya make -A
```

Аналогично можно передать адрес своего инстанса YQL:
```bash
CUSTOM_LOCAL_YQL=localhost:<your YQL port> CUSTOM_LOCAL_YT=localhost:<your YT port> ya make -A
```

{% note warning "Attention" %}

Локальный YQL сложно подружить с локальным YT. Для упрощения запуска есть [специальный инструмент](https://a.yandex-team.ru/arc_vcs/maps/tools/local_yt_yql), который запускает одновременно локальный YT и YQL.
Порты меняются при каждом запуске инструмента. Инструмент печатает первую часть команды с правильными портами, поэтому её можно скопировать из вывода.

{% endnote %}

## Тесты всего модуля целиком

Допустим модуль, который нужно протестировать, называется `mymodule`
и зависит от модулей `othermodule1` и `othermodule2`.

Тест всего модуля позволяет проверить:

* корректность интеграции с ресурсами других модулей
* корректность графа тасок
* выполнение всех тасок

### Импорты

```python
from maps.garden.libs import test_utils

from maps.garden.modules.othermodule1.lib import othermodule1
from maps.garden.modules.othermodule2.lib import othermodule2
from maps.garden.modules.mymodule.lib import mymodule
```

### Инициализация графа тасок

Для этого применяется вспомогательный класс `GraphCook`:

```python
TEST_REGIONS = [("cis1", "yandex")]

def test_module(environment_settings):
    cook = test_utils.GraphCook(environment_settings)

    othermodule1.fill_graph(cook.input_builder())
    othermodule2.fill_graph(cook.input_builder())

    mymodule.fill_graph(cook.target_builder(), TEST_REGIONS)
```

### Входные ресурсы

1. Создать питонячий объект нужного типа и добавить ему свойства. Пример:
```python
input_resource = cook.create_input_resource("input_resource_name")
input_resource.version = Version(properties={
    "param": "value"
})
```

2. Обеспечить наличие данных в ресурсе.
Можно физически создать необходимые данные. Пример:
```python
DATA = [
    {"id": 1, "data": "aaa"},
    {"id": 2, "data": "bbb"}
]

input_resource.write_table(DATA)
```
Можно замокать получение данных. Пример:
```python
@pytest.fixture
def remote_dir_mock():
    with open(yatest.common.source_path("some/path")) as f:
        with mock.patch('maps.garden.sdk.resources.remote_dir.urlopen', return_value=f):
            yield
```

### Запуск модуля

```python
result = test_utils.execute(cook)
```

#### NYT::Initialize {#nytinitialize}

Если в модуле есть хотя бы одна таска, которая запускает
MR-операции *напрямую из C++ API*, то в `PEERDIR` тестового `ya.make`
нужно добавить `mapreduce/yt/initialize`.

Это не касается YQL-тасок или тасок, запускающих MR-операций через
Python API.

## Тесты отдельных тасок

### Входные ресурсы

Создать входные ресурсы:

1. Создать питонячий объект нужного типа и добавить ему свойства. Пример:
```python
input_resource = yt_plugin.YtTableResource(
    name="resource_name",
    path_template="/resource_path/{region}",
    server="hahn")
input_resource.version = Version(properties={"region": "test_region"})
input_resource.load_environment_settings(environment_settings)
```
2. Обеспечить наличие данных в ресурсе аналогично тому, как описано выше.
3. Выполнить фиксацию ресурсов при необходимости:
```python
input_resource.logged_commit()
input_resource.calculate_size()
```

### Выходные ресурсы

Для выходных ресурсов достаточно выставить свойства и загрузить `environment_settings`:

```python
output_resource = yt_plugin.YtTableResource(
    name="output_resource_name",
    path_template="/output_resource_path/{region}",
    server="hahn")
output_resource.version = Version(properties={"region": "test_region"})
output_resource.load_environment_settings(environment_settings)
```

### Запуск таски

```python
task = MyTask()
task.load_environment_settings(environment_settings)
task(**input_resources, **output_resources)
```

Также см [NYT::Initialize](#nytinitialize)

### Хелперы для тестирования отдельных тасок
#### fixture test_task_executor

Упрощает создание типичного теста таски, сокращая количество кода для создания ресурсов и проверки результатов.

Пример:
```python
@pytest.mark.use_local_yt_yql
def test_my_example_task(test_task_executor):
    create_ymapsdf = test_task_executor.create_ymapsdf_input_yt_table_resource
    create_custom = test_task_executor.create_custom_input_yt_table_resource

    test_task_executor.execute_final_task(
        task=MyExampleTask(),
        input_resources={
            "ad": create_ymapsdf("ad"),
            "custom_table": create_custom("custom_table"),
        },
        output_resources={
            "out_table": test_task_executor.create_yt_table_resource("out_table"),
        },
    )
```
В примере выше создаются ресурсы для ymapsdf таблицы `ad`, пользовательской таблицы `custom_table`, выходной таблицы `out_table`. Исполняется задача `MyExampleTask` и проверяется выходной ресурс.
Данные для входных и ожидаемых выходных ресурсов должны располагаться в поддиректориях теста:
```properties
data/
  test_my_example_task/
    input/
      ad.jsonl
      custom_table.jsonl
    output
      out_table.jsonl
    schemas/
      custom_table.json
```

Данный хелпер позволяет также тестировать цепочку тасок, указывая в качестве входных ресурсов выходные ресурсы другой.

{% note warning %}

`test_task_executor` в данный момент ограничена созданием входных и выходных ресурсов только с типом `YtTableResource`.

{% endnote %}

## Использование YT-таблиц в тестах

### Входные таблицы в тестах

Записать данные в таблицу можно с помощью стандартной функции `write_file`.
В классе `YtTableResource` есть обёртка над этой функцией:

```python
DATA = [
    {"id": 1, "data": "aaa"},
    {"id": 2, "data": "bbb"}
]

input_resource.write_table(DATA)
```

Альтернативный способ - хранить данные в jsonl-файлах.
Каждая строка такого файла - это независимый json-объект, соответствующий строке таблицы.
Пример:

```
{"id": 1, "data": "foo"}
{"id": 2, "data": "bar"}
```

Функция [populate_resource_with_data](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs/test_utils/data.py?rev=6130111#L12) позволяет прочитать файл и записать его в таблицу ресурса:

```python
populate_resource_with_data(resource, input_data_path, table_name)
```

Здесь `input_data_path` - путь к директории с набором jsonl-файлов.
Предполагается, что одной таблице соответствует один файл, и его имя `<table_name>.jsonl`.

В Огороде часто приходится работать с геометрией.
В тестах геометрию удобно хранить в человекочитаемом формате WKT, но в YT-таблицах геометрия хранится в hex-encoded EWKB.

Функция `populate_resource_with_data` умеет на лету конвертировать  WKT -> EWKB -> hex.
Пример входного jsonl-файла с геометрией:

```
{"id": 1, "shape": "POLYGON((0 0,0 1,1 1,1 0,0 0))"}
```

По умолчанию имя колонки с геометрией - `shape`, но можно указать имя другой колонки.

Полностью создание входного ресурса `YtTableResource` выглядит так:

```python
resource = cook.create_input_resource(resource_name)
resource.version = Version(properties=properties)
resource.server = "hahn"
resource.load_environment_settings(cook.environment_settings)
resource.set_schema(schema)
populate_resource_with_data(resource, input_data_path, table_name)
resource.logged_commit()
resource.calculate_size()
```

Эта последовательность шагов обёрнута в функцию [create_yt_resource](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs/test_utils/data.py?rev=6237269#L13).

### Выходные таблицы

После того, как таска отработала, нужно проверить, что выходные таблицы из таски содержат ожидаемые данные.

Ожидаемые данные можно хранить в jsonl-файлах аналогично входным данным.

Функция [read_table_from_file](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs/test_utils/data.py?rev=6237269#L52) читает файл, попутно конвертируя геометрию WKT -> EWKB -> hex.

Пример проверки выходных данных:

```python
result_data = list(yt_client.read_table("path"))
expected_data = read_table_from_file(data_dir, table_name)

assert result_data == expected_data
```

Если таблиц много, то их все можно проверить разом с помощью одной функции
[validate_data](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs/test_utils/data.py?rev=6237269#L83)

### Таблицы ymapsdf в YT

Если ваш модуль принимает на вход `ymapsdf`, то можно использовать ряд полезных функций.

Вместо того чтобы линковать тесты к модулю `ymapsdf`, чтобы вызвать `fill_graph`,
можно использовать специальную версию функции `fill_graph` из библиотеки `maps/garden/libs/test_utils`:

```python
from maps.garden.libs.test_utils import ymapsdf

ymapsdf.fill_graph(cook.input_builder(), TEST_REGIONS)
```

Чтобы создать ресурсы и заполнить данными таблицы в локальном YT,
можно использовать функцию `create_final_resources`:

```python
ymapsdf.create_final_resources(
    cook,
    table_names=["ad", "ad_nm"],
    data_dir=yatest.common.test_source_path("input"))
```

Если вы хотите создавать таблицы вручную, то будет полезен класс
[YmapsdfSchemaManager](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs/test_utils/ymapsdf_schema.py?rev=6188446#L11),
который позволяет получить схемы для всех YT-таблиц.

Нужно добавить в `ya.make`:

```
DATA(arcadia/maps/doc/schemas/ymapsdf/garden)
```

## Использование ecstatic в тестах

Класс [EcstaticApiMock](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs/test_utils/ecstatic.py?rev=r7705269#L32) эмулирует поведение ecstatic и позволяет тестировать таски, которые работают с ecstatic.

Поддерживаемые сценарии:
* upload новой версии датасета из таски
* download датасета в таску
* активация датасета в ветке

Чтобы включить эмулятор ecstatic, нужно использовать фикстуру `ecstatic_mock` в тесте.

Структура теста выглядит так:
* Регистрация датасета (аналог конфига ecstatic)
* Опциональное добавление версии датасета (для тестов скачивания данных или активации)
* Создание огородного ресурса `DatasetResource` (для тестов скачивания данных или активации)
* Запуск таски или всего графа тасок
* Проверка результата

Пример:
```python
# declare dataset and possible branches
ecstatic_mock.register_dataset(dataset_name, branches=["testing", "stable"])

# [optional] add a new dataset version with stub data
ecstatic_mock.create_dataset_version(
    dataset_name=dataset_name,
    dataset_version=dataset_version,
    files=[],
    branches=["+testing"]
)

# [optional] add a new dataset version with real data
ecstatic_mock.create_dataset_version(
    dataset_name=dataset_name,
    dataset_version=dataset_version,
    files=[DatasetFile(filename="data.mms", content=b"HelloWorld")],
    branches=["+testing"]
)

# [optional] create an input Garden resource via GraphCook
test_utils.ecstatic.create_dataset_resource(
    cook,
    dataset_name,
    properties={"release_name": dataset_version}
)

# execute tasks
result = test_utils.execute(cook, enable_processes=False)

# make some assertions
branch_state = ecstatic_mock.get_dataset_branch(dataset_name, branch="stable")
assert branch_state.active_version == dataset_version
```

## PostgreSQL

Ресурсы и таски для работы с PostgreSQL временно не поддерживаются. Для использования
PostgreSQL в тестах следует использовать библиотеку `maps/garden/libs/test_utils_postgresql`

# Написание нового модуля

Есть 3 модуля-образца, которые соответствуют 3м типам модулей (`map`, `reduce`, `deployment`):
* [example_map](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/example_map)
* [example_reduce](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/example_reduce)
* [example_deployment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/example_deployment)

Чтобы создать новый модуль, можно взять любой образец, скопировать его и поправить везде имя модуля.

Ниже подробнее объясняется структура модуля, и как "с нуля" реализовать новый модуль.

## Постановка задачи

На вход модулю подается один ресурс, который является таблицей на YT. В таблице есть строковое необязательное поле `name`.
У ресурса есть одно обязательное свойство `shipping_date`.

Задача модуля - выбрать из таблицы разные значения поля `name`, начинающиеся с текста `aaa`,
записать в выходную таблицу в столбец `my_column` и посортировать.

Предполагается, что входной ресурс создается следующим кодом модуля `example_module_src`:
```python
def fill_graph(graph_builder, regions):
    graph_builder.add_resource(
        YtTableResource("example_module_src", "/path/to/yt/table", server="hahn")
    )
```

## Создание файловой структуры модуля

В папке `arcadia/maps/garden/modules` создадим подпапку с именем нового модуля `example_module` с такими файлами:

```text
./bin
./bin/main.py
./bin/ya.make
./defs
./defs/__init__.py
./defs/ya.make
./lib
./lib/graph.py
./lib/tasks.py
./lib/ya.make
./sedem_config
./sedem_config/__all__.yaml
./sedem_config/filters.yaml
./tests
./tests/tests.py
./tests/ya.make
./a.yaml
./module_traits.json
./README.md
./ya.make
```

## Реализация задач

Код задач должен быть реализован в классе-наследнике `maps.garden.sdk.core.Task`.
Необходимо как минимум реализовать метод `__call__` (подробнее про задачи описано [здесь](task.md)).

Файл `lib/tasks.py`:

```python
from maps.garden.sdk.core import Task
from maps.garden.sdk.yt.utils import ensure_equal_server


class SimpleTask(Task):
    def __call__(self, example_module_src, example_module_out):
        # Check that the in and out tables are located on the same YT cluster
        ensure_equal_server(example_module_src, example_module_out)

        # Assume that the input table has column `name`.
        # Filter values that start with "aaa".
        names = set()
        for row in example_module_src.read_table(columns=["name"]):
            name = row["name"]
            if name and name.startswith("aaa"):
                names.add(name)

        # Write filtered data to the output table
        example_module_out.write_table([{"my_column": name} for name in names])

        # Set key columns. This property will trigger table sorting on the resource commit.
        example_module_out.key_columns = ["my_column"]
```

## Построение графа задач

Файл `lib/graph.py`:

```python
from maps.garden.sdk.core import MutagenGraphBuilder, Demands, Creates
from maps.garden.sdk.extensions.property_propagators import EnsureEqualProperties
from maps.garden.sdk.yt import YtTableResource
from maps.garden.modules.example_module.lib import tasks


# graph building function doesn't have to be fill_graph, see below
# It takes one mandatory argument `graph_builder` and one optional argument `regions`.
def fill_graph(graph_builder, regions):

    # Propagate property "shipping_date" from the input to output resource.
    # This property will be used in the YT path template.
    graph_builder = MutagenGraphBuilder(
        graph_builder,
        property_propagator=EnsureEqualProperties(["shipping_date"]))

    # The output resource is an YT table with one required string column "my_column".
    example_module_out_resource = YtTableResource(
        name="example_module_out",
        # Path_template denotes a parametrized relative path of the output table.
        # The absolute path will depend on the environment where the task is executed.
        # E.g. for environment=datatesting and shipping_date=12345 the path will be
        # "//home/maps/core/garden/datatesting/example_module/12345"
        path_template="/example_module/{shipping_date}",
        schema=[
            {
                "name": "my_column",
                "type": "string",
                "required": True
            }
        ])

    # Each resource should be added to graph.
    graph_builder.add_resource(example_module_out_resource)

    # To add tasks we should specify how input and output resources are mapped to
    # arguments of call method: arguments of Demands and Creates constructors correspond
    # to __call__ method arguments.
    graph_builder.add_task(
        Demands(example_module_src="example_module_src"),
        Creates(example_module_out="example_module_out"),
        tasks.SimpleTask())
```

Файл `lib/ya.make`:

```text
PY3_LIBRARY()

OWNER(g:example-arcanum-team)

PY_SRCS(
    graph.py
    tasks.py
)

END()
```

## Создание исполняемого модуля

Файл `bin/ya.make`:

```text
PY3_PROGRAM(example_module)

OWNER(g:example-arcanum-team)

PEERDIR(
    maps/garden/sdk/module_rpc
    maps/garden/modules/example_module/lib
)

PY_SRCS(
    MAIN main.py
)

RESOURCE(
    ../module_traits.json /module_traits.json
)

END()
```

Файл `bin/main.py`:

```python
from maps.garden.libs.module_rpc import module_runner
from maps.garden.modules.example_module.lib import graph


def main():
    module_runner.run_module("example_module", graph.fill_graph)
```

## Экспорт имён ресурсов

Чтобы другие модули могли импортировать и использовать выходные имена ресурсов,
их можно разместить в отдельной небольшой библиотеке в папке `defs`.

Файл `defs/ya.make`:

```text
PY3_LIBRARY()

OWNER(g:example-arcanum-team)

PY_SRCS(
    __init__.py
)

END()
```

Пример файла `defs/__init__.py`:

```python
from maps.garden.sdk.extensions import resource_namer

NAMER = resource_namer.ResourceNamer(module_name="example_module")
```

## Описание свойств модуля

В файле `module_traits.json` определяем свойства модуля.

```json
{
    "name": "example_module",
    "displayed_name": "Example Module",
    "module_maintainer": "user_name",
    "type" : "map",
    "sources": ["example_module_src"]
}
```

Здесь описано, что модуль `example_module` использует ресурсы, создаваемые `example_module_src`.
Тип модуля `map` означает, что на каждый билд `example_module_src` можно запустить билд модуля `example_module`.
Такие модули отображаются в UI на вкладке `Shipping`.
`module_maintainer` - логин пользователя, ответственного за модуль.
Подробности описания модулей можно найти [здесь](module.md).

Файл `ya.make` имеет стандартный для всех модулей вид:

```text
OWNER(g:example-arcanum-team)

RECURSE(
    bin
    defs
    lib
    tests
)
```

{% note info %}

Указание `OWNER` нужно для того, чтобы изменение настроек модуля попадало на ревью владельцам модулей, а не команде Огорода.

{% endnote %}

## Файл README.md

Ответить на вопросы:

* Что делает модуль, какие данные варит.
* Какие данные принимает на вход.
* Кто является потребителем тех данных, которые варит модуль.
* Требования к свежести данных; что произойдёт, если новых данных не будет несколько дней.
* Как проверить, что модуль варит корректные данные.
* Как чинить поломки модуля.

После этого файл нужно добавить в документацию Огорода:
* Прописать путь до файла в [ya.make документации](https://a.yandex-team.ru/arc_vcs/maps/garden/docs/ya.make) в секции `DOCS_INCLUDE_SOURCES`
* Прописать название раздела и путь до файла README в [конфигурации документации](https://a.yandex-team.ru/arc_vcs/maps/garden/docs/toc.yaml) в секции "Описание модулей"

## Создание конфига Sedem

Для деплоя модуля нужно завести конфиг Sedem (подробнее про деплой [здесь](module-lifecycle.md)).

Файл `sedem_config/__all__.yaml`:

```yaml
main:
    name: example-module  # Имя main.name в конфиге Sedem должно быть написано через '-'.
    abc_service: example-service-name  # Имя abc-сервиса, к которому относится модуль
    subsystem: garden

deploy:
    type: garden
```

{% note warning "Attention" %}

Если в указанном `abc_service` будут люди с ролью `maps_garden_module_developer`, то они будут указываться наблюдателями:
* в тикетах, создаваемых при падении билдов модуля
* в тикетах MAPSLSR, связанных с модулем

{% endnote %}

Файл `sedem_config/filters.yaml`:

```yaml
alerts:
  - body:
      notifications:
        - type: telegram
          login: [example-chat-name]  # Чат команды разработчиков модуля
          status: [WARN, CRIT]
```

## Автосборка модуля

Покоммитная автосборка модуля осуществляется через новый CI и конфигурируется через файл `a.yaml`.

Файл `a.yaml` нужно сгенерировать с помощью Sedem. Подробности в [документации Sedem](https://docs.yandex-team.ru/sedem/releases#autobuild).

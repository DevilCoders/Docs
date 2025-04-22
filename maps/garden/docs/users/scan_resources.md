# Сканирование ресурсов из внешнего источника

Огород устроен так, что на вход каждому билду необходимо подать какие-либо ресурсы.
Для source-билдов существует специальный механизм получения ресурсов.

## Как использовать
При написании модуля можно в функцию `run_module`, по аналогии с `fill_graph`, передать опциональный аргумент
`scan_resources`.
Аргумент должен быть функцией, которая выполняет поиск ресурсов в какой-либо внешней системе и добавляет их в Огород.

Сигнатура функции:
```python
def scan_resources(environment_settings: Dict) -> Iterator[SourceDataset]
```

`SourceDataset` определён в `maps.garden.sdk.resources.scanners` и представляет из себя набор из `foreign_key` и списка ресурсов `BuildExternalResource` (этот класс не относится к огородным ресурсам).

{% note warning %}

Для автоматического запуска билдов от полученных ресурсов обязательно задание поля `sort_options` в `module_traits.json` с порядком сортировки отличным от `sort_by_build_id`.

{% endnote %}

Далее Огород упорядочит полученные из итератора датасеты опираясь на `sort_options` в `module_traits.json`.
И для первого (или группы первых датасетов при указании `builds_grouping` в `module_traits.json`), создаст билд, граф которого указан в параметре `fill_graph` у функции `run_module`, подав ему на вход ресурсы из списка.

## Особенности реализации
* Механизм с получением ресурсов работает только для модулей, у которых в `traits` указан тип модуля `source`.

* Необходимо указывать `foreign_key`.
`foreign_key`  - это словарь из строк в строки, необходимый для однозначного определения списка ресурсов для избежания
создания билдов из одинакового набора входных ресурсов.
Главное условие, налагаемое на `foreign_key` - уникальность для каждого набора ресурсов. Огород поддерживает уникальность
этого ключа для каждого контура и для каждого модуля.

{% note tip "Пример" %}

Для ресурсов из Sandbox можно так определить `foreign_key`:
```python
foreign_key = {"sandbox_resource_id": str(resource["id"])}
```

{% endnote %}

{% note warning %}

Код функции для получения ресурсов выполняется на сервере, поэтому не стоит реализовывать в ней вычисления
сложнее, чем листинг директорий в Yt или ресурсов в Sandbox.
Функция должна получать только метаданные, необходимые для создания объекта ресурса в Огороде.
Функция не должна пытаться работать с самими ресурсами: работа с ресурсами выполняется [тасках](task.md).

{% endnote %}

* Огород вызывает функцию получения ресурсов по умолчанию каждые 15 минут для каждого модуля, у которого реализовано сканирование ресурсов.
Для задания периода сканирования можно указать в файле `module_traits.json` индивидуальное расписание секундах:
```json
"scan_resources": {
  "period_sec": <time in seconds>
}
```
И для каждого нового датасета регистрирует `foreign_key`.
После запускает билд от первого датасета в порядке задаваемом `sort_options` из `module_traits.json`, если включен автостартер и такого билда ещё нет.

Билды от остальных датасетов можно запустить вручную через UI.

Также к таким билдам применяются все ограничения, задаваемые полем `build_limits` из `module_traits.json`.

Если необходим запуск нескольких билдов (например по билду на каждый регион), то необходимо в `module_traits.json` указать в поле `builds_grouping` список свойств `BuildExternalResource`, по которым будет производиться группировка. В таком случае будет запущен (если билда ещё нет и включен автостартер) первый билд из каждой группы.


{% note warning %}

Свойства, по которым производится группировка, должны быть заполнены в каждом `BuildExternalResource` из списка ресурсов в датасете. И в рамках одного датасета должны совпадать.

{% endnote %}


## Дополнительные возможности
Механизм с автоматическим получением ресурсов работает только для `stable` и `testing` контуров.
В пользовательских контурах или же для отладки можно вручную выполнить однократное сканирование ресурсов для конкретного
модуля. Для этого необходимо нажать на кнопку в UI Огорода на страничке модуля.

Так же для отладки можно вручную добавлять ресурсы в Огород. Описание есть на [этой](experiments#scenarij:-zapusk-src-modulya) странице.

Каждый запуск сканирования вручную или автоматически логируется. Посмотреть результаты запуска можно на
страничке:
```
https://garden.maps.yandex-team.ru/<contour_name>/<module_name>/auto-events
```
Ссылка и статус последнего сканирования есть на странице модуля в UI Огорода.

## Пример реализации
В файле `main.py`:
```python
from lib import fill_graph, scan_resources

def main():
    run_module("some_module", fill_graph, scan_resources=scan_resources)
```

Для удобства реализации в `maps.garden.sdk.resources.scanners` реализованы сценарии сканирования ресурсов в YT и Sandbox: `scan_yt` и `scan_sandbox`.

**Пример 1**: Проверяем директорию в Yt в поисках новых таблиц и просто регистрируем их в Огороде для следующих билдов.

В файле `lib.py`:
```python
import typing as tp
from yt.wrapper.ypath import ypath_split

from maps.garden.sdk.resources.scanners import scan_yt, SourceDataset



YT_PATH = "//home/maps/some/folder/path"
DATASETS_LIMIT = 5
RESOURCE_NAME = "some_resource_name"


def fill_graph(builder, unused_regions=None):
    builder.add_resource(
        yt_plugin.YtSourcePathResource(RESOURCE_NAME, server=YT_SERVER))


def _get_properties(yt_path):
    _, table_name = ypath_split(yt_path)
    return {
        "release_name": table_name[:10],  # YYYY-MM-DD
        "yt_path": yt_path,
    }


def scan_resources(environment_settings) -> tp.Iterator[SourceDataset]:
    return scan_yt(
        environment_settings=environment_settings,
        yt_base_path=YT_PATH,
        yt_nodes_limit=SCAN_LIMIT,
        get_garden_resource_properties_func=_get_properties,
        get_garden_resource_name_func=lambda path: RESOURCE_NAME
    )
```

**Пример 2**: Проверяем директорию в Yt в поисках новых поддирректорий. Каждая поддериктория — отдельный датасет, каждая из вложенных таблиц — отдельный ресурс.

```python
import typing as tp
from yt.wrapper.ypath import ypath_join, ypath_split

from maps.pylibs.yandex_environment import environment as yenv

from maps.garden.sdk import yt as yt_plugin
from maps.garden.sdk.resources.scanners import scan_yt, SourceDataset


YT_TABLE_TO_RESOURSE_NAME = {
    'table_name1': 'resource_name1',
    'table_name2': 'resource_name2',
}
DATASETS_LIMIT = 5
YT_PATH = "//home/maps/some/folder/path"
YT_PATH_SYMLINK = 'latest'


def fill_graph(builder, unused_regions=None):
    for resource in YT_TABLE_TO_RESOURSE_NAME.values():
        builder.add_resource(
            yt_plugin.YtSourcePathResource(resource, server=YT_SERVER)
        )


def _get_internal_paths(yt_path: str) -> tp.Iterator[str]:
    for table in YT_TABLE_TO_RESOURSE_NAME.keys():
        yield ypath_join(yt_path, table)


def _get_resource_properties(yt_path: str) -> dict[str, tp.Any]:
    dataset_yt_parht, _ = ypath_split(yt_path)
    _, release_name = ypath_split(dataset_yt_parht)
    return {
        "release_name": release_name,
        "yt_path": yt_path,
    }


def _get_resource_name(yt_path: str) -> str:
    _, table_name = ypath_split(yt_path)
    return YT_TABLE_TO_RESOURSE_NAME[table_name]


def scan_resources(environment_settings) -> tp.Iterator[SourceDataset]:
    return scan_yt(
        environment_settings=environment_settings,
        yt_base_path=YT_PATH,
        yt_nodes_filter=lambda node: node != YT_PATH_SYMLINK,
        yt_nodes_limit=DATASETS_LIMIT,
        yt_get_internal_paths=_get_internal_paths,
        get_garden_resource_properties_func=_get_resource_properties,
        get_garden_resource_name_func=_get_resource_name
    )

```


**Пример 3**: Сканируем ресурсы в Sandbox с группировкой по аттрибутам

```python
import typing as tp

from maps.masstransit.configs.feeds import config

from maps.garden.sdk.resources import RemoteDirResource
from maps.garden.sdk.resources.scanners import scan_sandbox, SourceDataset


RESOURCE_NAME_TEMPLATE = "resource_{}"
DATASETS_LIMIT_PER_CITY = 2
SANDBOX_RESOURCE_TYPE = "MAPS_MASSTRANSIT_GTFS_SOURCE"
SANDBOX_TASKS_OWNER = "MAPS-MASSTRANSIT"


def fill_graph(graph_builder, unused_regions=None):
    for region in config.FeedsConfig().all_regions():
        graph_builder.add_resource(RemoteDirResource(RESOURCE_NAME_TEMPLATE.format(region)))


def _get_resource_properties(dataset: dict[str, tp.Any]) -> dict[str, tp.Any]:
    return {
        "file_list": [
            {
                "name": "gtfs_data",
                "url": dataset["http"]["proxy"],
                "md5": dataset["md5"]
            }
        ],
        "shipping_date": dataset["time"]["created"],
        "region": dataset["attributes"]["city"]
    }


def scan_resources(environment_settings) -> tp.Iterator[SourceDataset]:
    for city in config.FeedsConfig().all_regions():
        yield from scan_sandbox(
            environment_settings=environment_settings,
            sandbox_attrs_filter={"city": city, "released": "stable"},
            sandbox_resource_type=SANDBOX_RESOURCE_TYPE,
            sandbox_owner=SANDBOX_TASKS_OWNER,
            get_garden_resource_properties_func=_get_resource_properties,
            get_garden_resource_name_func=lambda dataset: (
                RESOURCE_NAME_TEMPLATE.format(dataset["attributes"]["city"])),
            limit=MAX_GTFS_DATASETS_PER_CITY
        )
```

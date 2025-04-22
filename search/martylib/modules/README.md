# Модульная система
Модульная система `martylib` позволяет подключать gRPC-сервисы, интервалы и команды в качестве модулей к `search.martylib.modules.Daemon`.

После подключения модульной системы твой бинарник научится делать так:
```
$ ./binary run Server ApiService           # gRPC-сервер и gRPC-сервис
$ ./binary run shell                       # IPython
$ ./binary run -- background -ApiService   # группа модулей `background` без модуля `ApiService`
```

## Встроенные модули
`martylib` предоставляет набор встроенных и готовых к использованию модулей:
* [IPython](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/modules/module.py?rev=6598752#L211)
* IDM

Также предоставляются базовые классы для популярных сценариев:
* [gRPC-сервер](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/modules/module.py?rev=6598752#L180)
* [Raft](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/raft/base.py?rev=6598752#L125)


## Подключение
Для того, чтобы подключить модули проекта к `Daemon` нужно:
* импортировать python-модули с необходимыми модулями
* передать аргументы программы в `Daemon` (аргумент должен называться `modules`)

Пример:
```python
import argparse

from search.martylib.modules import Daemon

from my_project.modules import *  # Project-specific module imports.


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('modules', nargs='*', default=['shell'])
    args = parser.parse_args()

    Daemon(args=args).run()
```

Если аргумент со списком модулей называется `modules`, больше ничего делать не надо.

### gRPC-сервис
Этот способ используется для подключения имплементаций [Horadric](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2)-based сервисов.
Пример:
```python
from search.martylib.modules import ServiceModule

from my_project.services.my_project import ApiServiceInterface


class ApiService(ApiServiceInterface):
    ...


class ApiServiceModule(ServiceModule):
    @classmethod
    def get_service(cls):
        return ApiService()
```

### Команда
Команды запускаются **вместо** остальных модулей.


Команды могут быть терминирующими и нетерминирующими.
Терминирующие команды предотвращают настройку других модулей.

Только одна команда может быть исполнена при запуске `Daemons`.

Пример:
```python
from search.martylib.modules import CommandModule


class SayHello(CommandModule):
    @classmethod
    def run(cls):
        print('Hello, World!')
```

### Интервал
```python
from search.martylib.modules import LoopModule
from search.martylib.threading_utils import Interval


class MyAwesomeLoops(LoopModule):
    @classmethod
    def get_loops(cls):
        yield Interval(...)
        yield Interval(...)
        ...
```

Для совмещения с gRPC-сервисом можно использовать `ServiceAndLoopModule`:
```python
from search.martylib.modules import ServiceAndLoopModule

from my_project.services import ApiService


class MyAwesomeApi(ServiceAndLoopModule):
    @classmethod
    def get_service(cls):
        return ApiService()

    @classmethod
    def get_loops(cls):
        yield cls._get_service().some_interval
        yield cls._get_service().another_interval
```

## Группы модулей
Модули можно группировать с помощью [`search.martylib.modules.groups.ModuleGroups`](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/modules/groups.py?rev=6895363#L7).
Пример подключения:
```python
from search.martylib.modules.groups import ModuleGroups

from my_service.modules import ServerModule, ApiServiceModule


GROUPS = ModuleGroups()
GROUPS['background'] = {
    'ServerModule',
    'ApiServiceModule',
}
```

Пример запуска:
```
$ ./binary run background                         # запустит `ServerModule` и `ApiServiceModule`
$ ./binary run -- background -ApiServiceModule    # запустит только `ServerModule`
```

## Настройка модулей
Любой модуль может быть настроен перед запуском.
Для определение настройки модуля нужно переопределить [метод `setup`](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/modules/module.py?rev=6598752#L103).

Например, перед стартом `ApiServiceModule` можно подготовить БД:
```python
from search.martylib.db_utils import prepare_db


class ApiServiceModule(ServiceModule):
    @classmethod
    def setup(cls):
        prepare_db()
```

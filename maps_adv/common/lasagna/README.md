# Lasagna
Бойлерплейт для сервисов на базе `aiohttp`, `pgswim`, `warden`, `aiotvm`.

## Сбор слоев приложения
Основная точка расширения - метод `_setup_layers`. Принимает инстанс сконфигурированной базы данных (для сервиса с БД), обязан возвращать инстанс приложения aiohttp.
В этом методе производится вся основная работа по настройке слоев приложения - настройка клиентов к внешним сервисам, конфигурирование других частей, сбор api.
```python
from aiohttp import web

from maps_adv.common.lasagna import Lasagna

from .api import create as create_api


class Application(Lasagna):
    SWIM_ENGINE_CLS = None

    async def _setup_layers(self, db: None) -> web.Application:
        return await create_api()
```

## Конфигурирование и запуск
Конфиг передается в конструктор приложения как словарь, всегда доступен в `self.config`.
Для запуска приложения достаточно вызвать `run()`.
```python
from . import Application

app = Application({"SETTING": "VALUE"})
app.run()
```

## Подключение БД
Достаточно указать сабкласс `SwimEngine` в атрибуте `SWIM_ENGINE_CLS`.
При запуске приложения экземпляр будет сконфигурирован, используя строку подключения из опции конфига `DATABASE_URL`. Если указать `SWIM_ENGINE_CLS = None`, приложение будет инициализировано без базы данных.
Для нужд тестирования и отладки можно передать свой экземпляр БД, явно вызвав у инстанса приложения `setup(db)`.
```python
from aiohttp import web

from maps_adv.common.lasagna import Lasagna
from maps_adv.common.pgswim import SwimEngine

from .api import create as create_api


class Application(Lasagna):
    SWIM_ENGINE_CLS = SwimEngine

    async def _setup_layers(self, db: SwimEngine) -> web.Application:
        return await create_api()
```

## Автоматические миграции
Перед запуском приложения будет автоматически выполняться автоапргрейд БД с помощью `maps_adv.common.pgswim.Migrator`.
Путь к миграциям указывается в атрибуте `MIGRATIONS_PATH`.
Чтобы отключить автоматические миграции, необходимо выставить параметр `DB_AUTOMIGRATE` в `False`. 

## Настройка периодических задач
Периодические задачи управляются надзирателем [Warden](https://a.yandex-team.ru/arc/trunk/arcadia/maps_adv/warden).
Задачи указывается как словарь `{имя задачи: async callable}` в атрибуте `TASKS`. Имя задачи - зарегистрированное имя в сервере Надзирателя.
По умолчанию каждая задача при вызове получит `warden.client.lib.TaskContext` в качестве аргумента. Для передачи других аргументов необходимо указать их в `TASKS_KWARGS_KEYS` и установить в экземпляр приложения. 
Для включения задач необходимо в конфиге указать адрес сервера параметром `WARDEN_URL` и перечислить включаемые задачи параметром `WARDEN_TASKS`.
```python
from aiohttp import web

from maps_adv.common.lasagna import Lasagna
from maps_adv.common.pgswim import SwimEngine

from .api import create as create_api


async def some_task(context, config, db):
    pass


class Application(Lasagna):
    SWIM_ENGINE_CLS = SwimEngine

    TASKS = {"some_task": some_task}
    TASKS_KWARGS_KEYS = ["db", "config"]

    async def _setup_layers(self, db: SwimEngine) -> web.Application:
        self.db = db
        return await create_api()
```

## Настройка TVM клиента
`aiotvm.TvmClient` клиент может быть настроен автоматически и будет доступен в `self.tvm`, если в конфиге указаны валидные значения `TVM_DAEMON_URL` и `TVM_TOKEN`. Если одно из значений не указано или `None`, то `self.tvm is None`
```python
from aiohttp import web

from smb.common.aiotvm import TvmClient
from maps_adv.common.lasagna import Lasagna

from .api import create as create_api


class Application(Lasagna):
    SWIM_ENGINE_CLS = None

    async def _setup_layers(self, db: None) -> web.Application:
        assert isinstance(self.tvm, TvmClient)
        return await create_api()
```

## Логгирование для всего
Лазанья содержит фикстуру для глобальной настройки логгинга. Достаточно вызвать ее перед запуском приложения.
```python
from maps_adv.common.lasagna import setup_logging

from . import Application

setup_logging()
app = Application({})
app.run()

```

## Настройка TVM middleware
Лазанья может настроить проверку сервисных тикетов в запросах, если сконфигурирован TVM клиент. Можно управлять этим следующими способами:
1. Через декоратор `@tvm_auth.only`, указав имя параметра конфига со списком разрешённых tvm_ids. 
2. Через параметр конфига `TVM_WHITELIST` (последовательность чисел идентификаторов сервисов). Будет использован для всех ручек, которые не управляются первым способом.

В обоих случаях, если требуемый список пустой или не сконфигурирован, то запрос будет отклоняться с кодом возврата 403 и логироваться ворнинг. 


## Плагин pytest
Если подключить плагин `smb.common.aiotvm.pytest.plugin` и объявить фикстуру `app` (экземпляр сабкласса `Lasagna`), становится доступной фикстура `api`. Если приложение использует БД, необходимо объявить фикстуру `db`, которая возвращает экземпляр `pgswim.SwimEngine`.
Фикстура позволяет кратко кодировать protobuf запроса и декодировать тело ответа в указанный protobuf. С api фикстуры проще ознакомиться по коду `pytest/plugin.py` или примерам тестов.
```python
import pytest

from myapp import Application


@pytest.fixture
def app():
    return Application({})



async def test_api(api):
    got = api.get("/some_url/", expected_status=200)

    assert got == "Yo bro"
```

## Сенсоры и Solomon
Лазанья подключает в приложение хэндлер `/sensors/` для Соломона. Метрики определяются словарем SENSORS, где ключ - имя метрики (лэйбл `metric_group`), значение - билдер сенсора. По умолчанию включены и автоматически собираются метрики `rps`, `response_time`, `warden_tasks` и `logging`. Хаб метрик доступен как атрибут `sensors` из `_setup_layers`. Интеграцию с сенсорами можно полностью отключить установив `SENSORS` в `None`.
```python
import aiohttp

from maps_adv.common.lasagna import Lasagna
from smb.common.sensors import RateBuilder


class Resources:
    def __init__(self, hub):
        self.hub = hub

    async def handle(self, *args, **kwargs):
        self.hub.take("writes", label="value").add(10)
        return aiohttp.web.Response(status=200)


class App(Lasagna):
    SENSORS = dict(writes=RateBuilder(), **Lasagna.SENSORS)

    async def _setup_layers(self, db):
        resources = Resources(self.sensors)
        _api = aiohttp.web.Application()
        _api.add_routes([aiohttp.web.get("/kek/", resources.handle)])
        return _api
```

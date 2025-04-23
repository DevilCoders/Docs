# Config loader
Штука для загрузки конфига из переменных окружения, .env файла и [yav](https://yav.yandex-team.ru/).

```python
from maps_adv.common.config_loader import ConfigLoader, Option

config = ConfigLoader(
    Option("KEY_1"),
    Option("KEY_2", load_from="KEY_100", default=True),
    Option("KEY_3", converter=int),
)
config.init()

assert config["KEY_1"]
assert config.get("KEY_2")
assert "KEY_3" in config
```

## Как работает
Лоадер загружает необходимые параметры из доступных адаптеров один раз при вызове `.init()` и хранит в своем стэйте. Если какой-то из параметров не найден и нет дефолтного значение, произойдет исключение `OptionNotFound`, если какой-то из адаптеров не может быть инициализирован по ряду причин, будет записано сообщение в лог уровня warning.


## Про параметры
Параметры описываются как набор `Option`, где первый аргумент - имя, `load_from` - откуда загружать (по умолчанию используется имя), `default` - опциональное дефолтное значение, `converter` - callable (не применяется для default).


## Про конвертеры
Для ряда стандартных случаев в библиотеке есть предопределенные конвертеры, каждый из которых реализует callable. Для испльзования его достаточно передать аргументом `converter` в `Option`.
```python
from maps_adv.common.config_loader import ConfigLoader, Option, converters

config = ConfigLoader(Option("KEY", converter=converters.Tuple(int, delimiter=";")))
config.init()

assert config["KEY"]
```

- `converters.Bool()` конвертирует строку в булевое значение.
```python
assert converter.Bool()("1") is True
assert converter.Bool()("true") is False
assert converter.Bool()("0") is False
assert converter.Bool()("false") is False
assert converter.Bool()("null") is False
```

- `converters.Tuple()` конвертирует строку с разделителем в кортеж элементов.
```python
assert converter.Tuple()("first, second, third") == ("first", "second", "third")
assert converter.Tuple(int, delimiter=";")("1;2;3") == (1, 2, 3)
assert converter.Tuple(converter.Bool(), delimiter="-")("1-0-true-false") == (True, False, True, False)
```


## Про адаптеры
По дефолту поставляется три адаптера в порядке приоритета (высший - сверху)

- `OsEnvAdapter` читает переменные окружения
Читает параметры из переменных окружения, не трубует конфигурации.

- `DotEnvAdapter`
Читает параметры из .env файла, где каждая строка имеет формат key=value. Пустые строки и комментарии # будут проигнорированы.
```toml
KEY_1=value
KEY_2=0
KEY_3=100500
#KEY_4
```
По умолчанию файл ищется в рабочей директории, через переменную окружения `DOTENV_PATH` можно указать кастомный путь к файлу.
Если файл не найден, то адаптер будет пропущен с записью сообщения в лог.

- `YavAdapter`
Читает параметры из секрета в [yav](https://yav.yandex-team.ru/), требует указания параметров `YAV_TOKEN` и `YAV_SECRET_ID`. Параметры могут быть указаны в любом из более приоритетных адаптеров - как переменные окружения или содержимое .env-файла.
Если параметры не указаны, то адаптер будет пропущен с записью сообщения в лог.


#### Как написать свой адаптер
Все адаптеры наследуются от `BaseAdapter`, реализация требует только метод `load(self, key: str) -> str`.
Адаптер может опционально принимать настройки в конструктор `__init__`, которые должны быть описаны как кортеж `Option` в атрибуте класса dependencies.
```python
class AwesomeAdapter(BaseAdapter):
    dependencies = (Option("TOKEN"), Option("SOME_ID", default="kek"))

    def __init__(self, kek_token, lol_id):
        pass

    def load(self, key):
        return "azaza"
```

Классы адаптеров следует передавать как аргумент `adapters` в конструктор `ConfigLoder`, приоритет слева-направо. Дефолтные адаптеры использоваться не будут, только переданный набор.
```python
config = ConfigLoader(
    Option("KEK"),
    adapters=(OsEnvAdapter, AwesomeAdapter),
)
```

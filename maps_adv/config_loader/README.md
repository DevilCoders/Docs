# Config loader

Простая библиотека для чтения конфигурации из переменных окружения и файлов.

## Пример использования

```python
import os

from maps_adv.config_loader import Config

os.environ["WITHOUT_DEFAULT"] = "some_value"
os.environ["WITH_CONVERSION"] = "123"

config = Config(
    {
        "WITHOUT_DEFAULT": {},
        "WITH_DEFAULT": {"default": "default_value"},
        "WITH_CONVERSION": {"default": 100500, "converter": int},
    }
)

config.init()  # load configuration into config object

assert config.WITHOUT_DEFAULT == "some_value"
assert config.WITH_DEFAULT == "default_value"
assert config.WITH_CONVERSION == 123
```


## Конфигурация

* Параметры загрузки конфигурации указываются как словарь при инстанцировании `Config`
```python
config = Config({"OPTION": {}})

config.init()

assert config.OPTION == "some_value_from_env_or_file"
```

* Дефолтное значение может быть указано в ключе `default`
```python

config = Config({"OPTION": {"default": "default_value"}})

config.init()

assert config.OPTION == "default_value"

```

* Преобразование типа может быть указано в ключе `converter` как любой callable,
возвращающий ожидаемый тип
```python
config = Config({"OPTION": {"converter": int}})

config.init()

assert config.OPTION == 123
```

* Дефолтные значение никогда не конвертируются с помощью `converter` и возвращаются как есть
```python
config = Config({"OPTION": {"default": None, "converter": int}})

config.init()

assert config.OPTION == None
```

* Загрузка конфигурации (чтение .env файла и переменных окружения) выполняется только
при вызове `.init()`.
```python
from maps_adv.config_loader import Config, ConfigValueNotSet

config = Config({"OPTION": {}})

try:
    config.init()
except ConfigValueNotSet:
    print("Because OPTION does not set")
```

* Значение переменных окружения имеет высший приоритет при чтении конфигурации
```bash
#.env
OPTION=envfile_value
```

```python
config = Config({"OPTION": {}})

os.environ["OPTION"] = "env_var_value"
config.init()

assert config.OPTION == "env_var_value"
```

* При загрузке можно указать кастомный путь до файла конфигурации, иначе будет загружен
`.env` из текущей рабочей директории (если он есть)
```python
config = Config({"OPTION": {}})

config.init("/tmp/dir/another/dir/some/file/with/settings")
```

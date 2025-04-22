# Common dependencies of taxi projects on Python 3

## Installation

### Ubuntu

You can directly install `taxi-deps-py3-2` with `apt` utility:

```
sudo apt install taxi-deps-py3-2
```

### From scratch

You may want to install deps-py3 into your local virtualenv:

```
# From pypi
pip install -i https://pypi.yandex-team.ru/simple/ taxi_deps_py3_2

# From local copy
pip install -i https://pypi.yandex-team.ru/simple/ .

# Or directly from arcadia
pip install -i https://pypi.yandex-team.ru/simple/ svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/taxi/deps-py3
```

## Run linters/formatters

#### in all repository / only on changed files
* `make check-pep8`  / `make smart-check-pep8` - python linter
* `make format` / `make smart-format` - taxi formatter

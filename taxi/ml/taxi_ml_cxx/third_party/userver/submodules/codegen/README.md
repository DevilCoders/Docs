# Codegen

## Installation requirements

### Ubuntu

You can install all dependencies with package `taxi-deps-py3-2` with `apt` utility:

```
sudo apt install taxi-deps-py3-2
```

### From scratch

You can install dependencies from requirements file:

```
pip3 install -i https://pypi.yandex-team.ru/simple/ -r requirements.txt 
```

## Run linters/formatters (need [taxi-deps-py3](https://github.yandex-team.ru/taxi/deps-py3#installation))

#### in all repository / only on changed files
* `make check-pep8`  / `make smart-check-pep8` - python linter
* `make format` / `make smart-format` - taxi formatter

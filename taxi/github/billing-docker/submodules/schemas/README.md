# Yandex.Taxi Schemas

See https://wiki.yandex-team.ru/taxi/backend/datastorage/ for details.

How to add configs: https://wiki.yandex-team.ru/taxi/backend/architecture/configs/Manual/#rabotasyamlfajjlami

## Environment setup

Install [taxi-deps-py3](https://github.yandex-team.ru/taxi/deps-py3#installation) for using formatters.

Setup environment using virtualenv:

```
virtualenv --python=python3.7 .env
. .env/bin/activate
pip install -r requirements.txt

# Test your installation
make test
```

## Run tests

`make test`

## Run linters/formatters (need [taxi-deps-py3](https://github.yandex-team.ru/taxi/deps-py3#installation))

#### Run in all repository / run only on changed files
* `make check-pep8`  / `make smart-check-pep8` - python linter
* `make format` / `make smart-format` - taxi formatter

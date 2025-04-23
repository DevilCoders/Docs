# Как перевести свой Nile-скрипт на Nile over YQL?
При сборке Nile-скрипт собирается в обычный исполняемый бинарь, а вот при Nile over YQL соберет файл с расширением `*.so`, который нужно запускать с помощью специальной библиотеки [Python UDF](https://yql.yandex-team.ru/docs/yt/udf/python/).

Для nile создан специальный запускатор [run_python_udf](https://arcanum.yandex-team.ru/arc/trunk/arcadia/yql/tools/run_python_udf) и интегрерирован в `ya nile`, т.е. для запуска нужно использовать `ya nile`.

## Python3
Предположим, что есть скрипт на Nile, использующий в качестве бекенда YT (по умолчанию).

### Nile
`main.py`:
```python
from nile.api.v1 import cli

@cli.statinfra_job()
def main(job, options):
    job.table('/path/to/input/table') \
         ...
        .put('/path/to/output/table')

    return job

if __name__ == 'main':
    cli.run()
```

`ya.make`:
```
PY3_PROGRAM()
OWNER(login)
PEERDIR(
    statbox/nile
)
PY_SRCS(
    MAIN main.py
)
```

Сборка и запуск производится следующим образом:
```
$ ya make
$ ./<binary> run --proxy hahn ...
```

### Nile over YQL
Перепишем его, чтобы в качестве бекенда использовался YQL.

В скрипте `main.py` немного меняется структура:
```python
from nile.api.v1 import cli

@cli.statinfra_job()
def make_job(job, options):
    job.table('/path/to/input/table') \
         ...
        .put('/path/to/output/table')

    return job

def main:
    cli.run()
```
и также способ запуска в `ya.make`:
```
YQL_PYTHON3_UDF(nile_over_yql_job)
REGISTER_YQL_PYTHON_UDF(
    NAME CustomPython3
)
OWNER(login)
PEERDIR(
    statbox/nile
    yql/library/python
)
PY_SRCS(
    MAIN main.py
)
```

Запуск также будет производиться по-другому:
```
$ ya make
$ ya nile ./*.so -- run --use-yql --proxy hahn ...
```

### Что ещё необходимо будет менять
#### 1. Явно указывать типы создаваемых колонок
Было
```
job.table('/path/to/input/table') \
    .project(
        has_deep_use=ne.custom(int, 'has_deep_use')
    )
```
Стало
```
job.table('/path/to/input/table') \
    .project(
        has_deep_use=ne.custom(int, 'has_deep_use').with_type(int),
    )
```

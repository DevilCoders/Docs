# Пример приложения на основе нового фреймворка Stapler

Пример содержит два приложения.
- Приложение для построения графа `graph_generator`
- Основное исполняемое приложение с полезным кодом, который будет исполняться в Nirvana `calculator`

## CI/CD

Проект подключен к новой системе CI/CD аркадии.
Тестовый pipeline запускается автоматически на каждый PR

Релизный пайплайн запускается вручную
- https://a.yandex-team.ru/ci/alpaca/releases/timeline?dir=market%2Fmonetize%2Fstapler%2Fexample&id=stapler-example-release

Проект в Nirvana
- https://nirvana.yandex-team.ru/project/stapler_example/flows/1/filter?@filterName=All&projectId=ExprStringEquals(ec257407-a509-4066-888d-8d3d0c43774d)&@sorting=created%3Atrue

Реакция запуска production
- https://reactor.yandex-team.ru/browse?selected=7962549

## СОБРАТЬ
    cd ~/arc/arcadia/market/monetize/stapler/example
    ya make -r --yt-store ./graph_generator
    ya make -r --yt-store ./calculator

## ЗАПУСТИТЬ graph_generator

`graph_generator` основное приложение для сборки и публикации графа
У тестового приложения добалено свое CLI тля тестов.
Обратите на это внимание. При запуске `graph_generator` нужно будет указать свои параметры.

    cd ~/arc/arcadia/market/monetize/stapler/example
    ./graph_generator/graph_generator

### CLI graph_generator

Пример CLI, в вашей реализации его можно менять и оно может быть другим

```
cd ~/arc/arcadia/market/monetize/stapler/example
./graph_generator/graph_generator --help

usage: graph_generator [-h] [--log-level LOG_LEVEL] [--secret_name SECRET_NAME] [--yt_token YT_TOKEN] [--proxy PROXY] [--pool POOL] [--quota QUOTA]

optional arguments:
  -h, --help            show this help message and exit
  --log-level LOG_LEVEL, -l LOG_LEVEL
                        log level
  --secret_name SECRET_NAME, -s SECRET_NAME
                        Nirvana secret name
  --yt_token YT_TOKEN, -t YT_TOKEN
                        YT token
  --proxy PROXY         YT proxy [hahn, arnold...]
  --pool POOL, -p POOL  pool default=<username>
  --quota QUOTA, -q QUOTA
                        Nirvana quota
```

## ЗАПУСТИТЬ calculator

`calculator` основное исполняемое приложение с полезным кодом.
У приложения `calculator` автоматически формируется CLI которое можно тестировать локально

    cd ~/arc/arcadia/market/monetize/stapler/example
    ./calculator/calculator

### CLI calculator
Автоматическое собранное CLI приложения `calculator`

```
cd ~/arc/arcadia/market/monetize/stapler/example
./calculator/calculator --help

Usage: calculator [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  Task1
  Task2


./calculator/calculator Task1 --help

Usage: calculator Task1 [OPTIONS]

Options:
  --param2 TEXT  Очень нужный параметр param2  [required]
  --param1 TEXT  Очень нужный параметр param1  [required]
  --help         Show this message and exit.
```

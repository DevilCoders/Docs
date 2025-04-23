# Приложение граф-генератор для проекта Алгоритмов Репленишмента

На базе Stapler.v2

- https://a.yandex-team.ru/arc/trunk/arcadia/market/monetize/stapler/v2

## Wiki мониторинга

- https://wiki.yandex-team.ru/market/replenishment/alpaca_monitorings/

## Проект Алгоритмов Репленишмента

- https://a.yandex-team.ru/arc/trunk/arcadia/market/replenishment/algorithms

## Проект в Nirvana

- https://nirvana.yandex-team.ru/browse?selected=9347797

## build

Собрать

    ya make --yt-store

## main cli

    ./monitoring --help

    Usage: monitoring [OPTIONS] COMMAND [ARGS]...

    Options:
      -l, --log TEXT  logging level
      --help          Show this message and exit.

    Commands:
      graph
      run

## graph cli

Деплой графа в нирвану

    ./monitoring graph --help

    Usage: monitoring graph [OPTIONS]

## run cli

Локальный запуск задач

    ./monitoring run --help

    Usage: monitoring run [OPTIONS] COMMAND [ARGS]...

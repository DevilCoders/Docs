# Мониторинг для партнерского интерфейса

В этом репозитории находится набор классов, которые запускаются по крону.
Классы выполняют некоторые проверки и результаты этих проверок отправляют
в juggler.

## Собрать образ

  ./build

## Запуск тестов

  ./run_tests

  ./run_tests self_update

## Запуск контейнера

  ./run

## Апдейт зависимостей

  update_deps

  ./build

## Выкладка
Раскатывать нужно с той же ветки! Если запускаем ansible ноута, а делали правки на dev, то нужно сделать checkout 

  ansible -i ./hosts -m include_role -a name=partner2-juggler-checks-dev dev4 -b

## Запуск проверки
  ./run
  DEBUG=3  /app/bin/run_check.sh   Check::NOL 2>&1 | less

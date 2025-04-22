# Основной проект команды алгоритмов replenishment
Проект с кодогенерацией графа в Nirvana для расчета рекомендаций пополнения складов.
Основная часть работы графа это подготовка данных для оптимизатора `ALPACA` (vicugna).

Результатом работы приложения кодо-генератора - граф в `Nirvana`, который запускается по расписанию с помощью реакции в `https://reactor.yandex-team.ru`
После успешного завершения расчета рекомендаций данные складываются на YT `https://yt.yandex-team.ru`

Сейчас проект активно переходит на фреймворк [Stapler](https://a.yandex-team.ru/arc/trunk/arcadia/market/monetize/stapler)

- Про [alpaca](https://wiki.yandex-team.ru/market/replenishment/alpaka-iz-roda-vikunevyx/)
- Основная страница проекта в [wiki](https://wiki.yandex-team.ru/market/replenishment/)

## Структура проекта
Сам проект содержит нескольких приложений.
- graph_generator
- alpaca (vicugna)
- common_calculator
- common_calculator_v2



```
root (./market/replenishment/algorithms)
__
  |__bin # бинарники
  |  |__graph_generator # python3 app
  |  |__common_calculator # python2 app
  |  |__common_calculator_v2 # python3 app
  |  |__vicugna # c++ bin
  |__lib # модуль python3
  |__lib23 # модуль python2
  |__vicugna # с++ либа для vicugna (alpaca)
```

## [graph_generator](./bin/graph_generator) `bin/graph_generator`
Главное приложение - точка входа. Имеет свой CLI, подготавливает и публикует граф

## [alpaca (vicugna)](./bin/vicugna) `bin/vicugna`
Приложение на `C++`

Подробнее тут
- https://wiki.yandex-team.ru/market/replenishment/alpaka-iz-roda-vikunevyx/

## [common_calculator](./bin/common_calculator) `bin/common_calculator`
`legacy`

Старое приложение "калькулятора" обработки данных.
Базируется на `NAIL` кубике Nirvana в связи с чем накладывает большие ограничения на возможности проекта (основная причина почему мы переходим на Stapler)

## [common_calculator_v2](./bin/common_calculator_v2) `bin/common_calculator_v2`
Новое приложение "калькулятора" на базе `Stapler`.
Раскрывает новые возможности в том числе использовать Spark, torch и позволяет писать "кубики" в нирвана для исполнения произвольного кода.

## CI/CD
Основной Flow в аркадии
- https://a.yandex-team.ru/projects/alpaca/ci/releases/timeline?dir=market%2Freplenishment%2Falgorithms&id=replenishment-main-ci

### Реакция ежедневных запусков графа
- https://reactor.yandex-team.ru/browse?selected=8588374

### Результаты Prod запусков
- https://nirvana.yandex-team.ru/flow/104da699-c386-44ac-af2d-cecbbeac0507/graph

### Stable draft
- https://nirvana.yandex-team.ru/flow/71b892ec-e4ff-4891-b2a0-c35cff957dc0/graph

### Stage/test запуски
- https://nirvana.yandex-team.ru/flow/13fe93a3-b4a0-4ba1-a295-acd263a8e91c/graph


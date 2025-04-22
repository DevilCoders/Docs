# Документация tenfifty

**Tenfifty** - библиотека для построения пайплайнов машинного обучения.

![Логотип](pic/tenfifty_logo.jpg)

## Краткое описание     {#description}

В основе библиотеки лежит небольшой набор «строительных блоков»,
из которых можно собирать сложные графы, включающие в себя препроцессинг данных,
обучение моделей, стэкинг, вычисление метрик и другие необходимые для ML операции.

Tenfifty включает в себя мощный yaml-конфигуратор, который позволяет строить пайплайны без написания кода.

Библиотека не заточена под Нирвану, но совместима с ней.

## Основные разделы документации    {#contents}

* [{#T}](quickstart.md)
* [{#T}](architecture.md)
* Бэкенды
  * [{#T}](backends/draw.md)
  * [{#T}](backends/nirvana.md)
  * [{#T}](backends/tape.md)
  * [{#T}](backends/dump_task.md)
* Конфигурация
  * [{#T}](configuration/parser.md)
  * [{#T}](configuration/api.md)
* Композитные действия
  * [{#T}](composite_actions/overview.md)
  * [{#T}](composite_actions/sequential_train.md)
  * [{#T}](composite_actions/iterative_train.md)
  * [{#T}](composite_actions/crosslearning_train.md)
* Плагины
  * [{#T}](plugins/overview.md)
  * [{#T}](plugins/yt.md)
  * [{#T}](plugins/yql.md)
  * [{#T}](plugins/executable_runner.md)
  * [{#T}](plugins/tabtools.md)
  * [{#T}](plugins/tlm.md)
  * [{#T}](plugins/catboost.md)
  * [{#T}](plugins/metrics.md)
  * [{#T}](plugins/storage.md)
* Демонстрации
  * [{#T}](demonstration/overview.md)
  * [{#T}](demonstration/train_tlm.md)
  * [{#T}](demonstration/train_catboost.md)
  * [{#T}](demonstration/sequential_task.md)
  * [{#T}](demonstration/crosslearning_task.md)
* [{#T}](contacts.md)

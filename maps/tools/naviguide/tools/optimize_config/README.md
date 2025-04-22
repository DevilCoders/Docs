# Оптимизатор конфига клиентской привязки
Тулза для подбора параметров конфига клиентской привязки [`maps/analyzer/libs/guidance/include/config.h`](/arc/trunk/arcadia/maps/analyzer/libs/guidance/include/config.h) разменивающая число ложных сходов на время детекции схода используя [симплекс-метод](https://en.wikipedia.org/wiki/Nelder%E2%80%93Mead_method).
В текущей реализации функция оценки корректирует число ложных сходов при помощи множителя определяемого временами детекции схода - слабо поощряет если ожидаемое время схода выдерживается или сильно штрафует в противном случае.

## Использование
```bash
.../pkg$ ./maps/tools/naviguide/tools/optimize_config/bin/optimize_config \
    --config /default.yson \
    --etalons //home/maps/jams/dev/users/jemdo/wip/optimize/etalons_2020-07-27 \
    --iterations 200 \
    --results //home/maps/jams/dev/users/jemdo/wip/optimize/iterations
```
Тулза зависит от оценки качества привязки [`maps/tools/navimatcher_quality`](/arc/trunk/arcadia/maps/tools/navimatcher_quality)

В конфиге оптимизатора задаются фиксированные и перебираемые параметры. Для фиксированных `fixed=%true` параметров указывается значение `value`, для перебираемых также указывается диапазон перебора `min, max` и шаг `step` для задания начального симплекса. 

В результате работы оптимизатора по целевому пути создаются таблицы оценки качества привязки дополненные атрибутом со значениями параметров конфига.

Также содержит вспомогательные тулзы:
  * [`tools/calc_quality`](tools/calc_quality) — считает качество отдельного результата (конфига) используя функцию оценки оптимизатора
  * [`tools/collect_iterations`](tools/collect_iterations) — собирает итерации в сводную таблицу для возможности удобной визуализации результата
  * [`tools/quality_checker`](tools/quality_checker) — перебирает все имеющиеся итерации оптимизации и находит итерацию с оптимальным значением функции оценки
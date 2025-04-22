# Оценка качества матчера для навигатора

## 0. Быстрый старт:

Сгенерировать эталоны и запустить рассчёт качества.

Сгенерировать эталоны:
```bash
./tools/etalon_generator/etalon_generator \
    --reports '//home/maps/jams/dev/navimatcher-quality/reports[#0:#1000]' \
    --target-path //home/maps/jams/dev/navimatcher-quality/19.07.16-0/etalons.1000 \
    --graph-version 19.07.16-0
```

Если исходная таблица содержит не отчёты в виде блобов (`MAPKITSIM`), а [таблицу с событиями](/arc/trunk/arcadia/maps/tools/naviguide/pylib/schema.py)  (см. например результат вывода [parse_blob](/arc/trunk/arcadia/maps/tools/naviguide/tools/parse_blob)), то можно передать и её с аргументом `--events '//home/maps/jams/dev/navimatcher-quality/19.07.16-0/etalons.1000/events'`

Запустить расчёт качества (актуальные конфиги [`naviguide`](/arc/trunk/arcadia/maps/tools/naviguide) в [`maps/tools/naviguide/conf`](/arc/trunk/arcadia/maps/tools/naviguide/conf)):
```bash
./tools/evaluate_quality/evaluate_quality \
    --etalons //home/maps/jams/dev/navimatcher-quality/19.07.16-0/etalons.1000 \
    --target //home/maps/jams/dev/users/voidex/results.1000 \
    --config conf/naviguide.cfg \
    --graph-version 19.07.16-0
```

Также можно указать аргументы:
* `--route-quality` — посчитать метрикой ложных сходов на основе перестроений
* `--quality-only` — не проводить симуляцию, просто пересчитать кач-во


### Известные проблемы (TODO?)

Сейчас признак нахождения на эталоне бинарный - на нём или нет. В этом случае возможны две "плохие" ситуации:
1. Произошёл скачок назад по эталону с потерей маршрута. Истинного схода согласно метрике не было, с эталона мы не уходили, это попадает в false detected losts, но по сути — ложный сход
2. Сошли с маршрута раньше, чем эталон, и задетектили сход. Истинного схода пока или уже (если вернулись обратно на маршрут) нет согласно эталону, с самого эталона мы также не уходили. Это попадает также в false detected losts, а по сути — истинный сход.

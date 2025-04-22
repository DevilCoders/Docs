### Plotter example

Пример на [plotter](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/plotter_lib), который можно копировать к себе и на его основе рисовать свои графики

Здесь в коде считаются запросы, где показывались колдунщики на веб-серпе,
А затем в YT в //tmp табличку сохраняется топ по показам колдунщика Картинок

Чекаут и сборка:
```
ya make -r --checkout analytics/plotter_example
cd analytics/plotter_example
```

Пример запуска:
```
./plotter_run.sh --date 2019-12-21 --token `cat ~/.yql/token` --1p
```
Или:
```
ya nile libplotter.so -- --date 2019-12-21 --token `cat ~/.yql/token` --1p
```

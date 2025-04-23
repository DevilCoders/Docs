# ytalloc_profiling_flame_graph_adapter 

## Зачем?
Утилита для подготовки результата профилирования YT аллокатора к построению flame graph-а. 

## Использование

```(bash)
    $ curl localhost:58001/profiled_allocations > profiled_allocations.yson
    $ cat profiled_allocations.yson | ./ytalloc_profiling_flame_graph_adapter | ./contrib/tools/flame-graph/flamegraph.pl --color=mem --title="Memory Usage in Bytes Flame Graph" --countname="bytes_used" > profiled_allocations.svg
```

Пример `profiled_allocations.yson`:  https://paste.yandex-team.ru/3131141

Результат применения: https://jing.yandex-team.ru/files/mafanasev/profiled_allocations.svg 

## Особенности
При профилировании собираются стеки глубиной не более 16 фреймов. Чем больше номер фрейма, тем ближе он к `main()`. Утилита группирует стеки по именам функций. Таким образом, два стека, у которых отличаются фреймы с номерами 17+, в результате сгруппируются в один, используемая память при этом суммируется.
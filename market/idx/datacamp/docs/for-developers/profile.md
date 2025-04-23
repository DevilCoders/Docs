## CPU-профилирование C++ приложений
### TLDR
1. В контейнере запускаем запись вызовов ``ya tool perf record -p `pgrep -x binary_name` --call-graph dwarf,65528 -c 4000000 -B -N -- sleep 30 && ya tool perf script > out.perf``. В место `binary_name` подставляем название нашего бинарника, например `miner`, `piper`, `stroller`.
2. Чтобы постоить красивый отчет, получившийся `out.perf` копируем на нашу дев тачку либо ноут `scp {hostname}:out.perf .`
3. Строим отчет `~/arcadia/contrib/tools/flame-graph/stackcollapse-perf.pl out.perf |  c++filt > out.folded && ~/arcadia/contrib/tools/flame-graph/flamegraph.pl out.folded > fgraph.svg`
4. Для интерактивного просмотра отчета можно открыть `fgraph.svg` через браузер. Пошарить результать с коллегами можно с помощью `ya upload fgraph.svg`

Инструкция собиралась из следующих источников:
* [Market Report Profiling with Perf](https://wiki.yandex-team.ru/market/report/infra/tech-faqs/market-report-profiling-with-perf/)
* [Профилирование по CPU с помощью perf (+ визуализация с помощью FlameGraph)](https://clubs.at.yandex-team.ru/arcadia/18242)
* [ya profile](https://wiki.yandex-team.ru/yatool/profile/)

## CPU-профилирование для python приложений
[py-spy](https://vdmit.at.yandex-team.ru/584)

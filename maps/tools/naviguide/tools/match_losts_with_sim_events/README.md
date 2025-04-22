Тулза для анализирования событий в эмуляции для моментов ложных сходов в проде

## Запуск
```bash
./match_losts_with_sim_events -g <guided> -p <prod_route_losts> -n <naviguide_route_losts> -o <output_table>
```
- `<guided>` - таблица симуляции `guided`: например, после запуска [`evaluate_quality`](/arc/trunk/arcadia/maps/tools/navimatcher_quality/tools/evaluate_quality) или [`evaluate_experiment`](/arc/trunk/arcadia/maps/tools/naviguide/tools/evaluate_experiment)
- `<prod_route_losts>` - таблица с интересующими продовскими сходами, в [таком](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/route-quality/route_lost&) формате
- `<naviguide_route_losts>` - таблица `route_quality/losts` - получается из `guided` после расчёта `route_quality`-качества

## Что оно делает
Для каждого ложного схода тулза собирает статистики по событиям в симуляции, которые происходили в окне +-`indent` секунд от этого ложного схода.

`--indent` - настраивает отступ, по умолчанию 20 секунд

### Краткий хелп по колонкам:

- `lost_time` - время ложного схода в проде (UTC+3)
- `lost_ts` - то же самое, только timestamp, для удобства дебага
- `sim_route_requests` - количество запросов маршрута в симуляции (в таблице `guided`)
- `sim_lost_type` - список итоговых сходов из route_quality/losts в симуляции
- `sim_no_route` - флажок отсутствия маршрута в симуляции на момент ложного схода. Для каждого репорта он сначала `true` и после первого события запроса маршрута (в окне) в guided навсегда становится `false`
- `sim_events` - это список статусов - того, что происходило, глядя на сигналы в таблице `guided`
- `not_on_route` - это событие `OnRoute->NotOnRoute->OnRoute` - "честная стрелка"
- `guided_lost` - это событие `OnRoute->[NotOnRoute*]->RouteLost->[NotOnRoute*]->OnRoute` - "сход"
- `route_finished` - это просто детект события `RouteFinished`. Все `RouteFinished` потом выкидываются и не портят расчёт честных стрелок и сходов
- `no_events` - флаг, что в окне совсем нет сигналов
- `on_route` - значит, что событий честных стрелок и сходов в окне нет
для дебага правильности расчёта `sim_events` есть колонка `debug` , в которую сложены сырые события (без повторений)
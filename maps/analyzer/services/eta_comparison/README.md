Сравнение качества предсказания eta c конкурентами
---

- [`logbroker/reader`](lib/logbroker/reader.py) компонент для чтения логов из logbroker-а
- [`logbroker/parser`](lib/logbroker/logbroker.py) парсеры логов из logbroker-а
- [`merger`](lib/merger.py) компонент для объединения логов навигатора и роутера
- [`proto_parser`](lib/proto_parser.py) компонент для парсинга маршрута из protobuf
- [`region_limiter`](lib/region_limiter.py) компонент ограничивающий число запросов для каждого региона
- [`eta_predictor`](lib/eta_predictors.py) предикторы eta конкурентов
- [`yt_uploader`](lib/eta_predictors.py) загрузчик предсказаний конкурентов в yt
- [`paths`](lib/paths.py) путь, куда загружается результат

Бинарник для запуска сравнения находится в директории [`bin`](bin)

Пример запуска
```bash
./eta_quality_cmp -c path_to_config -g path_to_geobase
```

Данные записываются в yt-таблицу, путь до которой описан в модуле [`paths`](lib/paths.py).<br>
Его можно перепределить, добавив секцию в конфиг:
```json
{
    "paths": {
        "EtaQualityCmpTool.LOGS": "//path-to-results"
    }
}
```

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_eta_comparison_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_eta_comparison_stable/) | [ core-eta-comparison.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-eta-comparison-stable-panel-main/) | [ maps_core_eta_comparison_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_eta_comparison_stable) |
[Monitorings all (tag=a_prj_maps-core-eta-comparison)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-eta-comparison) |

# Contributing

- `config/sandbox-ci.json` - конфигурация для запуска CI пайплайна ([подробнее](https://github.yandex-team.ru/search-interfaces/microservices/blob/master/services/sandbox-ci/docs/universal.md))
- `scripts/validate_configs.js` - скрипт для валидации конфигов
    - Выбран JS т.к. bash требует много предустановок
    - Должен возвращать результат в `txt_reports/report.txt` или `html_reports/index.html` форматах ([подробнее](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/market/front/MarketFrontCI/__init__.py?rev=r8275245#L24))

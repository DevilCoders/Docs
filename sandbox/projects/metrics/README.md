# CI/CD [Metrics](https://wiki.yandex-team.ru/JandeksPoisk/Metrics/)
Тут лежат скрипты для сборки метриксовых проектов в аркадии.
## [PPP](/arc/trunk/arcadia/search/scraper/parser_platform)
Платформа парсеров релизится при помощи sandbox таски `METRICS_PARSER_PLATFORM_ARCADIA_RELEASE` (код находится [тут](parser_release_arcadia/__init__.py)).

Изменения кода происходят следующим образом:
### Изменения в рамках `on_execute`
Для того что бы сделать изменения которые касаются внутренности метода `on_execute` достаточно поправить код, собрать его, и выложить при помощи собранного же кода:
``` sh
ya make
bin/bin upload --attr target=sandbox/metrics/bin --attr release=stable
```
Сама таска в sandbox в этом случае найдет последнюю версию бинаря и запустит ее.
### Изменения в других методах
Согласно [документации](https://wiki.yandex-team.ru/sandbox/quickstart/#test-tasks) sanbox.

Необходимо завести виртуалку, а дальше проверить что после комита проходят тесты.

# Саджест отелей

Саджест или поисковые подсказки выводятся пользователю при вводе запроса в строке поиска на владке отелей на портале путешествий.
Основная цель - сокращение времени пользователя.


## Описание работы

Источник поисковых подсказок - саджест отелей на базе [общеяндексовских технологий саджеста](https://wiki.yandex-team.ru/suggest/)


### Что происзодит при вводе пользователя

1. Фронт делает запрос к API фронта
2. API фронта делает запрос к API путешествий
3. API путешествий делают запрос к мультисаджесту на ручку `https://suggest-multi.yandex.net/hotels/suggest`
4. API парсит полученный ответ и обрезает его до лимита в соответствии со [спецификацией](https://github.yandex-team.ru/data-ui/ya-travel-spec/tree/master/hotels/suggest)
5. API отдает полученный саджест API фронта
6. API фронат отдает полученный саджест фронту


## Источники данных для саджеста
`
Данные для саджеста подготавливаются по следующей схеме:

1. [Билдер словарей саджеста отелей](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/suggest/builder) подготавливает текстовые словари саджеста.
2. [Билдер команды саджеста](https://a.yandex-team.ru/arc/trunk/arcadia/quality/trailer/suggest/data_builder) конвертирует текстовые словари в бинарный формат.
3. Полученнеы бинарные словари [публикуются в Sandbox](https://sandbox.yandex-team.ru/resources?owner=TRAVEL&type=SUGGEST_DICT&limit=20&attrs=%7B%22name%22%3A%22hotels%22%7D&created=6_months).
4. Этапы 1-3 реализованы в [pipeline](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/suggest/pipeline) и запускаются по распианию с помощью [sandbox_planner](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/sandbox_planner/), имя таски `hotel_suggest_build_pipeline`.
5. После выкатки ресурсов, они автоматически выкатываются в [тестинг мультисаджеста](https://nanny.yandex-team.ru/ui/#/services/catalog/suggest_multi_r1/).
6. В случае успешной выкатки словарей в тестинг мультисаджеста они катятся в [прод мультисаджеста](https://nanny.yandex-team.ru/ui/#/services/catalog/suggest_multi/).

Тестовые и продовые инстансы API путешествий настроены на прод мультисаджеста. Из-за этого у нас нет возможности выкатить тестовый словарь без изменения конфигурации API. 


## Метрики

Для измерения качества саджеста разработан компонент [metrics_builder](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/suggest/metrics_builder)

Компонент запускается по расписанию через [sandbox_planner](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/sandbox_planner/), имя таски `hotel_suggest_metrics_builder`.

Метрики публикуются в виде [сводной таблицы в dash](https://datalens.yandex-team.ru/wizard/krd2wmc3aykog-suggest-metrics-aggregated-svodnaya-tablica).

Виды метрик:
- `show` - по запросу показан какой-либо саджест
- `recall` - по запросу показан отель/регион, который запрашивал пользователь
- `recall_1` - по запросу показан регион/отель, который запрашивал пользователь, причем саджест был показан первым в списке
- `saved` - количество символов, которые пользователь сэкономит на вводе полного названия отеля/региона, если выберет саджест из подсказки
- `saved_1` - количество символов, которые пользователь сэкономит на вводе полного названия отеля/региона, если выберет саджест из подсказки, при этом саджест был показан первым в списке


## Чеклист выкатки новой версии саджеста

Сейчас выкатка саджеста настроена автоматически. В случае каких-то радикальных изменениях в схеме сборки данных необходимо

1. Собрать бинарные словари локально, вручную или с помощью [pipeline].
2. Запустить [web_fastcgi_daemon](https://a.yandex-team.ru/arc/trunk/arcadia/quality/trailer/suggest/web_fastcgi_daemon) с собранными бинарными словарями.
3. Настроить API на локальный web_fastcgi_daemon (опционально).
4. Проверить саджест через web_fastcgi_daemon или API.

После успешного тестирования новых данных можно закоммитить измнения в построителе словаря саджеста и перезапустить процессы сборки в проде и тестинге.

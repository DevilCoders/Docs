# PPP: как добавить свой парсер?

1. Написать парсер
2. Разместить парсер в Аркадии
3. Написать конфиг
4. Разместить конфиг в Аркадии

* * *

* Код PPP: [search/scraper/parser_platform](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform)
* README: [search/scraper/parser_platform/README.md](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/README.md)
* Пример: [search/scraper/parser_platform/example.md](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/example.md)

## Парсер

Парсер -- класс Python 2 в методом `parse`, который принимает строку (с HTML, JSON итп) и возвращает нужное объектное представление. 

Код парсеров хранится в Аркадии и собирается в бинарь с помощью `ya make`.

[Arcadia Starter Guide](https://wiki.yandex-team.ru/arcadia/starterguide/).

* * *

Если нужно будет потом обрабатывать результаты в Metrics, это представление должно соответствовать [формату Метрикса](https://wiki.yandex-team.ru/JandeksPoisk/Metrics/API/serp/#primeryjsonserpov).

* * *

В `parsers/base_parsers.py`доступны вспомогательные классы: `SerpParser`, в котором настроено логирование, и `JSONSerpParser`, дополнительно облегчающий работу с парсингом `JSON`.

* * *

Парсинг запускается как map-операция на YT, читающая из стандартного входа и пишущая в стандартный выход, в связи с этим возникают некоторые ограничения:

* Парсер не должен писать логов в стандартный выход.
* Сделать http-запрос во внешний мир не получится.

## Preparer

Перпарер -- так же класс, с методом `prepare`, который принимает запрос из корзинки запросов а так же дополнительные параметры и возвращает curl подобную строчку понятную SoY.
Предполагается что пользователь в своих классах не бдует напрямую формировать SoY запросы а будет переопределять вспомогательные методы из `SerpParser`: 
`_get_url_template` или просто `URL_TEMPLATE` что бы задать все кроме cgi,
`_prepare_cgi` для того что бы задать cgi.

### Тесты

Тесты находятся в `parser_platform/tests`. Перед написанием своих стоит взглянуть на [`parser_platform/tests/README.md`](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/tests/README.md). В качестве подробного примера можно взять [`search/scraper/parser_platform/tests/yandex_video_islands_json_parser_test.py`](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/tests/yandex_video_islands_json_parser_test.py).

### Deployment

Файл парсера нужно будет разместить в [`search/scraper/parser_platform/parsers`](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/parsers). Чтобы парсер попал в сборку, имя файла должно быть указано внутри PY_SRCS в [`search/scraper/parser_platform/parsers/ya.make`](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/parsers/ya.make). После этого CI прогонит тесты. Если они они пройдут, выполнит сборку бинарника и  разместит его на YT ([//home/qe/scraper/testing/ppp/](https://yt.yandex-team.ru/hahn/?page=navigation&path=//home/qe/scraper/testing/ppp/)).

## Конфиг

Пример конфига ([`search/scraper/parser_platform/search_engine_config/uslugi-profiru.json`](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/search_engine_config/yandex-baobab-html.json)):

```JSON
{
  "parser-config": {
    "type": "arcadia-python-parser-config",
    "classname": "YandexBaobabHTMLParser",
    "module": "yandex_baobab_html_parser",
    "preparer": "YandexBaobabHTMLParser",
    "output-format": "METRICS"
  }
}
```
`type` следует всегда выставлять в `arcadia-python-parser-config` (остальные варианты устарели). `module` - название модуля, `classname` - название класса парсера, `preparer` - название класса подготавливающего запрос.

### Deployment

Готовый конфиг нужно закоммитить в Аркадию: [search/scraper/parser_platform/search_engine_config/](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/search_engine_config/), 
после этого новый парсер автоматически прорастет в интерфейсе [сервиса экспериментов](https://metrics.yandex-team.ru/xp/new).

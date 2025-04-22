# Python Parser Platform
* [Howto](ppp_howto.md)
* [Пример парсера с интеграцией с Метриксом](example.md)

## Intro

Парсер преобразует некоторую строку (HTML, JSON, XML etc) в объектное представление.
Часто речь идет о поисковой выдаче. Платформа парсеров Python позволит желающим
самостоятельно писать, развертывать и править собственные
парсеры для [Scraper](https://wiki.yandex-team.ru/qe/scraper/) на Python 🐍.

## Requirements

Код написан на (аркадийном) Python 3 и собирается с помощью `ya make`.

## Интерфейс парсера

Парсер должен быть оформлен как класс, предоставляющий метод `parse`, который
принимает строку и возвращает результат в виде объекта (вероятно, комбинации стандартных
словарей и списков Python). Метод `parse` будет вызван многократно (для разных строк)
с один и тем же экземпляром парсера.
Если определен метод `__init__`, его должно быть можно вызвать без параметров.

В `base_parsers.py` лежат два вспомогательных класса:

* В общем случае можно отнаследоваться от класса `SerpParser`, в нем настроено логирование.
* Если надо разобрать данные в формате `JSON`, доступен класс `JSONSerpParser`,
* предоставляющий метод для безопасной навигации.

## Структура каталогов

Парсеры кладём в `parser_platform/parsers`. Внутри целесообразно создавать подкаталоги по сервисам.
Сейчас многие парсеры лежат прямо в корне, но их правильнее категоризировать.
Образец для подражания - каталог `parser_platform/parsers/yandex_baobab`.

### Интеграция с метриксом

Если парсер планируется использовать для скачек в [Метриксе](https://metrics.yandex-team.ru)
объект результат должен соответствовать [метриксовому формату](https://wiki.yandex-team.ru/metrics/api/serp/#primeryjsonserpov) без элемента query.
Например из парсера может вернуться следующий объект:
```(json)
{
  "components" : [ {
    "componentInfo" : {
      "type" : 1  #1 значит что это результат поиска (2 колдунщик)
    },
    "componentUrl" : {
      "pageUrl" : "http://ya.ru" # сюда можно положить url
    },
    "type" : "COMPONENT" # это надо что бы метрикс не запутался
  }],
  "text.customTextFiled": "custom value"
}
```

Чтобы Метрикс понял дополнительные поля, надо что бы они назывались в стиле `<type>.<name>` - где `type` понятен
метриксу. Например, это может быть `"text.myNewTextFiled": "textvalue"` или `"json.jsonField1": {"k": "v"}`.

* [Wiki описание метриксового формата](https://wiki.yandex-team.ru/metrics/API/serp/#format).
* [Wiki описание доступных типов](https://wiki.yandex-team.ru/metrics/API/serp/#dostupnyetipyrequirementov).

Исключение: количество документов нужно положить на верхнем уровне по ключу `"long.docsFound"`
(а не по `"headers" > "foundDocumentsCount"`, как можно предположить из документации по метриксовому формату).

## Mapper-обертка

Парсинг является map-операцией на YT, там же лежат таблицы с серпами.
У таблиц по историческим причинам есть несколько разных форматов.
Обертка читает входную таблицу, вынимает из нее нужную строку, запускает выбранный парсер
и укладывает результат в нужном формате. Хочется надеяться, что пользователю не понадобится разбираться,
как они устроены.

## Сборка

Парсеры с оберткой собираются в исполняемый бинарник (он будет называться `metrics`).
Для этого нужно в [arcadia/search/metrics/monitoring](https://a.yandex-team.ru/arc/trunk/arcadia/search/metrics/monitoring) выполнить команду:

```bash
ya make
```

Чтобы парсер попал в сборку, он должен быть указан внутри `PY_SRCS` в `parsers/ya.make`.

У утилиты `metrics` есть [множество команд](https://a.yandex-team.ru/arc/trunk/arcadia/search/metrics/monitoring/readme.md), в контексте парсинга интересна команда `parse`.

Для работы с некоторыми командами нужно [настроить окружение](https://a.yandex-team.ru/arc/trunk/arcadia/search/metrics/monitoring#настройка-окружения).

## Локальный запуск

Локально запустить парсинг выдачи без оберток можно с помощью опции `--parse-only`:
Для использования опции `--engine ClassMyParser` нужно в файле
`arcadia/search/scraper/parser_platform/parsers/preparer_mapping.py` импортировать свой парсер и в `ENGINES`
прописать filename.ClassMyParser

```bash
cat content.html | ./metrics parse local --engine YandexBaobabHTMLParser --parse-only
```

## Компактное представление

Во время разработки удобно видеть список компонет, не пропуская его через `jq`.

```bash
cat content.html | ./metrics parse local --engine YandexBaobabHTMLParser --compact
```

даст таблицу с некоторыми полями:

```
  no  type                       title                                                         pageUrl                                                       viewUrl
----  -------------------------  ------------------------------------------------------------  ------------------------------------------------------------  ----------------------------------------
   0  W: WIZARD_KNOWLEDGE_GRAPH  Электрическое напряжение
   1  W: WIZARD_SUGGEST_FACT     Формула нахождения напряжения: основные понятия ... -         https://220v.guru/fizicheskie-ponyatiya-i-                    220v.guru › ... › Напряжение
                                 220v.guru                                                     pribory/napryazhenie/formula-rascheta-napryazheniya-cherez-
                                                                                               silu-toka-i-soprotivlenie.html
   2  W: WIZARD_IMAGE                                                                          https://google.ru/search?source=univ&tbm=isch&q=%D1%84%D0%BE
                                                                                               %D1%80%D0%BC%D1%83%D0%BB%D0%B0+%D0%BD%D0%B0%D0%BF%D1%80%D1%8
                                                                                               F%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5&hl=ru&fir=svsMy_cWVvYe0M%252
                                                                                               CJnz52ZaOr5bnvM%252C_%253BQbGzOmjBv3IkOM%252CUotM6XPA64yHLM%
                                                                                               252C_%253BzUZPsj7F7oBTsM%252CaSN9tnELvAHYnM%252C_%253BIdWEcN
                                                                                               XEYocT5M%252CSfrvtIYvWmt7CM%252C_%253Bsjr7qH9zHEcrpM%252CKb_
                                                                                               4FKt1E9BoDM%252C_%253BZVsOji0QM690aM%252C3TdfET7-tvoLIM%252C
                                                                                               _%253B5MWtac_UvsQ5vM%252Cd5FVZcW4OsDcjM%252C_%253B1UTZQMrwDk
                                                                                               TJsM%252CPeWhOBuYBmOAJM%252C_
   3  SEARCH_RESULT              Напряжение, сопротивление, ток и мощность.                    http://sebestroj.ru/ehlektrosnabzhenie/naprjazhenie-          sebestroj.ru › ehlektrosnabzhenie
                                                                                               soprotivlenie-tok-moshhnost.html
```

## Локальный запуск с оберткой

Локально отпарсить некоторую таблицу:

```bash
yt read '//home/metrics/metrics_executable/examples/yandex_baobab_html_input' --format json --proxy hahn.yt.yandex.net | ./metrics parse local --engine YandexBaobabHTMLParser
```

## Запуск на YT

Отпарсить на YT некоторую таблицу:

```bash
./metrics parse yt --engine YandexBaobabHTMLParser \
--scr //home/metrics/metrics_executable/examples/yandex_baobab_html_input \
--dst //tmp/parsed_table
```

При работе не под Linux для выполнения команды `yt parse` требуется проделать [дополнительные шаги](https://a.yandex-team.ru/arc/trunk/arcadia/search/metrics/monitoring#работа-под-mac).

## Препареры

Как правило парсер имеет смысл вместе с рецептом построения запросов из содержания корзины.
Такой рецепт мы называем _препарером_. Препарер реализуется классом с методом `prepare`, это может быть класс парсера.
В `SerpParser` определен такой метод, обращающийся к полям `URL_TEMPLATE`/`TOUCH_URL_TEMPLATE` и
вспомогательным методам `_prepare_url`, `_prepare_headers`, `_prepare_cgi`, `_prepare_cookies`, `_prepare_userdata`,
задающим URL, заголовки и так далее. В конкретных препарерах достаточно переопределить их.
В качестве примера можно изучить `YandexBaobabParser`.

Посмотреть на получающиеся для корзины 307271 запросы можно так:

```bash
./metrics qg local 307271 | ./metrics prepare local yandex.ru --engine YandexBaobabHTMLParser
```

Более подробно команды для работы с препарерами можно изучить в [основной документации `metrics`](https://a.yandex-team.ru/arc/trunk/arcadia/search/metrics/monitoring#конвертация-запросов-для-прокачки-через-scraper-over-yt-soy) и встроеной справке.

Свой препарер нужно добавить в `parsers/preparer_mapping.py`. Ключ в отображении `MAPPING` -- это то, что передается
в аргумент `--engine`.

### Параметры запуска при использовании API Scraper

К параметрам созданных [через API](https://wiki.yandex-team.ru/qe/scraper/api/#acinxronnoezadanienabatchevujuskachkuzaprosov) скачек можно обратиться внутри препарера.

* Параметры батча (`per-set-parameters`) будут доступны в `additional_parameters.get("ssr", {}).get("per-set-parameters", {})`.
* Параметры запроса (`per-query-parameters`) -- в `basket_query.get("per-query-parameters")`.

## Конфиг для парсера

Пример [крона](https://metrics.yandex-team.ru/crons/102617/runs). В Monitoring Over Yt Cron v19 появилось поле
`Parse parameters`, туда прописываете конфиг в формате json.

В коде настройками можно пользоваться вот [так](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/parsers/yandex_baobab_parser.py?rev=6692946#L44).
Конфигурация будет доступна в методе ```parse``` и родственных как параметр [additional_parameters](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/wrapper/wrapper_lib.py?rev=r9131747#L56).

В локальном режиме запуск может выглядеть так:
```
./metrics parse local --parse-only --module yandex_baobab_html_parser --classname YandexBaobabHTMLParser --parser-config config.json
```
Где config.json это:
```json
{"dump_node":true}
```

## Тесты

Запуск всех тестов (из `search/scraper/parser_platform`):

```
ya make -tA
```

Запуск конкретного теста
```
ya make -tA -F yandex_baobab_html_with_custom_user_agent_parser_test.py
```

Подробнее см. в [tests/README.md](tests/README.md).

## Search Engine

Чтобы парсер можно было использовать в экспериментах и кубиках, нужно задать конфигурацию search engine:

```JSON
{
  "id": "yandex-baobab-html",
  "parser-config": {
    "type": "arcadia-python-parser-config",
    "classname": "YandexBaobabHTMLParser",
    "module": "yandex_baobab_html_parser",
    "preparer": "YandexBaobabHTMLParser",
    "output-format": "METRICS"
  }
}
```

Другие примеры можно посмотреть в папке [search_engine_config](search_engine_config), свой нужно положить
туда же, и Scraper подхватит конфиг автоматически после прохождения тестов в CI. Актуальные
search engine'ы можно посмотреть по ручке
[scraper.yandex-team.ru/api/scraper/engines/all](https://scraper.yandex-team.ru/api/scraper/engines/all)

Попробовать локально приготовить запрос воспользовавшить командой  [./try_prepare_custom](../cli_tools/README.md#fetch-query-group)

Также есть скрипт, которым можно быстро проверить конфиги в `search_engine_config`.
Просто запустите (без параметров, из каталога `parser_platform`) скрипт
```
./validate-search-engine-configs.py
```
Он пройдет по всем конфигам и проверит, что в них валидные имена модулей парсеров,
и они успешно импортируются. Потенциально могут быть проблемы, если в вашем парсере есть аркадийные импорты.
Для удобства их можно загнать под try-except, как например в yandex_baobab_html_parser.py

## CI/CD
Платформа парсеров подключена к автосборке, так что в целом за ними можно наблюдать в [CI](https://a.yandex-team.ru/projects/metric/ci).

Следить за выкладкой изменений можно в job'е [Release metrics binary to production](https://a.yandex-team.ru/projects/metric/ci/actions/launches?dir=ci%2Fregistry%2Fprojects%2Ftestenv%2Fmetrics&id=metrics-binary-release-prod).

После успешного заверешения задачи в Sandbox можно запускать [эксперименты](https://metrics.yandex-team.ru/xp/new) с новым парсером.

Если выкатка в CI упала из-за инфраструктурных проблем (например downtime yt кластеров hahn или arnold)
можно "докатить" изменения, нажав на упавшую задачу, затем "Open flow", затем рестарт нужного кубика.

## Misc
TSV-файлы tld-доменами в папке parsers/data стоит править консистентно с конфигурацией доменов в PRS.
см. https://a.yandex-team.ru/arcadia/history/search/scraper/parser_platform/parsers/data/README.md

### See also

Документация Metrics про баобабный парсер Yandex: https://wiki.yandex-team.ru/metrics/baobab/

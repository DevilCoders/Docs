## Пример парсера с интеграцией с Метриксом
Рассмотрим общую интеграцию с Метриксом на примере html баобабного парсера.

### Код
Код парсера лежит в модуле [yandex_baobab_html_parser](parsers/yandex_baobab_html_parser.py) в классе `YandexBaobabHTMLParser`, 
иерархия классов выгялдит так:  `YandexBaobabHTMLParser > YandexBaobabParser > YandexJSONSerpParser > JSONSerpParser > SerpParser`.

Для формирования curl запроса для html парсер переопределяет поле `EXP_FLAGS` который [используется при формировании cgi](parsers/yandex_baobab_parser.py?rev=6410621#L220) в базовом класе. 
Так же в родиельском классе [определен](parsers/yandex_baobab_parser.py?rev=6410621#L206) шаблон урла `URL_TEMPLATE` который формирует начало строки запроса (для тачей `TOUCH_URL_TEMPLATE`) 
Методы формирующие хедеры определены для всех яндексовых парсеров на уровне [YandexJSONSerpParser](parsers/base_parsers.py?rev=6410621#L631) методами `_prepare_headers_multimap` и `_prepare_cookies_multimap`.

Метод `_parse` определяет каким образом по html получить серпсет в [метриксовом](https://wiki.yandex-team.ru/JandeksPoisk/Metrics/API/serp/) формате 
(без запроса - он автоматически подставляется из запроса в корзинке). 
В случае если выдача в формате json достаточно определить `_parse_json` как это [сделано](parsers/yandex_baobab_parser.py?rev=6410621#L19) в базовом баобабном парсере.

### Конфигурация для scraper
Для того что что бы scraper правильно понял как пользоваться парсером есть [json конфиг](search_engine_config/yandex-baobab-html.json) описывающий модуль и классы парсера и препарера.

### Метрикс
На метриксе в кроновом эксперименте используется парсер по названию совпадающий с названием конфига, [пример крона](https://metrics.yandex-team.ru/crons/102243/runs).

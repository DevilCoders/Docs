# urls-by-show-counters

Класс для работы с данными из ресурса URLS_BY_SHOW_COUNTERS_DATA. Позволяет получать урлы, по которым была показана та или иная фича, используя её счетчик показа.
В данный содержит данные для `web4` и следующих платформ:
* `desktop` (по умолчанию),
* `touch (touch-phone)`,
* `pad (touch-pad)`,
* `searchapp`.

## ВНИМАНИЕ!

Нет никаких гарантий, что данные содержат урл, по которому действительно будет показана фича, потому что:
* По данной платформе фича с этим счетчиком ни разу не была показана за вчерашний день;
* За время, прошедшее с момента сбора данных, фича уже успела устареть для данного запроса (например, колдунщики спортивных трансляций);
* Фича может работать только для залогинов;
* Любые другие ограничения, не покрывающиеся только правильным url'ом;
* На момент конкретного открытия страницы гермионой, источник данных был недоступен.

## Как это работает

* По [шедулеру](https://sandbox.yandex-team.ru/scheduler/4864/view), раз в сутки, запускается sandbox-задача [URLS_BY_SHOW_COUNTERS](https://sandbox.yandex-team.ru/tasks/?order=-updated&type=URLS_BY_SHOW_COUNTERS&page=1&pageCapacity=20&forPage=tasks);
* В ней запускается вполне конкретная [MapReduce-операция](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/UrlsByShowCounters/executable/bin/main.py) в YT, которая берёт поисковый `blockstat`-лог за прошедшие сутки, строит таблицу с соответствием `counter -> platform -> url` ([примеры таблиц](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/fei/FEI-7133-features-by-counters)) и сохраняет в ресурс с типом [ABSOLUTE_URLS_BY_SHOW_COUNTERS_DATA](https://sandbox.yandex-team.ru/resources/?type=ABSOLUTE_URLS_BY_SHOW_COUNTERS_DATA&page=1&pageCapacity=20);
* Ресурс скачивается и используется этим классом.

### Переменные окружения

* `ABSOLUTE_URLS_BY_SHOW_COUNTERS_DATA_RESOURCE_PREPARED` отключит скачивание и обновление ресурса с данными при create/sync (предполагается, что он уже подложен по правильному пути);
* `ABSOLUTE_URLS_BY_SHOW_COUNTERS_DATA_DOWNLOAD_TIMEOUT` позволяет переопределить таймаут на скачивание данных (в миллисекундах);
* `ABSOLUTE_URLS_BY_SHOW_COUNTERS_DATA_RESOURCE_ID` позволяет указать конкретный ресурс с данными (по умолчанию используется последний).

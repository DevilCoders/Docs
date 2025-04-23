# CGI-параметры

* [Параметры, поддерживаемые репортом](http://zelo.serp.yandex.ru/all-supported-params)

* `&json_dump=1&init_meta=use-new-dump` — выводит все данные от репорта
* `&init_meta=use-new-dump` — включит новый актуальный дамп
* `&json_dump=searchdata.images`, `&json_dump=searchdata.clips` — выводит только данные по выдаче
* `&export=json` — выводит точные данные от репорта (не работает с темпларом), существуют и [другие отладочные флаги репорта](https://wiki.yandex-team.ru/serp/development/dump/)
* `&i-m-a-hacker=1` — имитирует запрос из внешней сети
* `&no_tests=1` — отключает все эксперименты
* `&user_time=YYYYMMDDHHMM` — подменяет время пользователя, например: `&user_time=201707260000`
* `&yandex_login=billy` — имитирует авторизованного пользователя с указанным именем
* `&promo=pumpkin` — включает тыкву (резервная версия на случай отказа бекендов)
* `&promo=nomooa` — выключает жучка
* `&lr=N` — регион, `&l10n=lang` — язык, возможные значения:
    * `&lr=213` — москва (`.ru`), язык - `&l10n=ru` - (можно не прописывать отдельно, он соответствует домену)
    * `&lr=157` — минск (`.by`), язык - `&l10n=be`
    * `&lr=143` — киев (`.ua`), язык - `&l10n=uk`
    * `&lr=162` — астана (`.kz`), язык - `&l10n=kk` (казахский) и `&l10n=tt` (татарский).
    * `&lr=11508` — истамбул (`.com.tr`), язык - `&l10n=tr` (можно не прописывать отдельно, он соответствует домену)
    * `&lr=87` — вашингтон (`.com`), язык - `&l10n=en` (можно не прописывать отдельно, он соответствует домену), для индонезийского (СПОК) - `&l10n=id`
* `&exp_flags=enable_fake_yandex_app_api;appsearch_header` — включение эмулятора мобильного поискового приложения, дополнительно нужно указать UserAgent:
    * Android: `Mozilla/5.0 (Linux; Android 4.4.2; SM-G900F Build/KOT49H) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/30.0.0.0 Mobile Safari/537.36 YandexSearch/4.45`
    * iOS: `Mozilla/5.0 (iPhone; CPU iPhone OS_8_2 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) YaApp_iOS/100`
    * Android Pad: `Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58K; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/47.0.2526.26 Mobile Safari/537.36 YandexSearch/4.70/apad`
* `&counterDebug=1` — вывести информацию об отправляемых счётчиках в консоль браузера
* `&counterDebug=notimer` — не выводить информацию о счётчиках таймера (для Видео)
* `&gridDebug=1` — вывести данные логирования сетки (для Картинок)
* `&eventDebug=*` — вывести информацию о подписываемых БЭМ-событиях в консоль браузера *(только в режиме development)*
* `&eventDebug=blockname` — вывести только подписки на указанный блок *(только в режиме development)*
* `&bem-profiler=1` — вывести время инициализации клиентских блоков

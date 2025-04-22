# Неофониши

Неофониши включаются экспериментом `domik-neophonish-exp-enable` (рубильник на 100%) и специфичным ориджином/маской для каждого сервиса. Конфиг тут https://github.yandex-team.ru/passport-frontend/core/blob/develop/passport/configs/common/index.js#L665

* `origins` - ориджины
* `originsMask` - маски

Есть возможность включить неофонишей не на 100%. Для этого существуют отдельные списки ориджинов/масок - `originsAB` и `originsMaskAB`. Под этими ориджинами/масками неофониши работают только если попасть в основной эксперимент и в один из двух дополнительных - `domik-neophonish-exp-ab-enable` (раскатан на тачи) или `domik-neophonish-exp-ab-control-desktop` (раскатан на десктоп).

Если нужно исключить ориджин из под маски, то его следует добавить в список `excludedOrigins`.

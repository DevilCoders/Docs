## RUM

Стандартный инструмент для отправки клиентских метрик. Подробнее: https://github.yandex-team.ru/RUM/rum-counter

Пример:

https://rum.yandex-team.ru/projects/market_front_desktop/compare?componentSettings=%7B%22compare%22:%7B%22resultTypes%22:[%22timemark.page.firstScreen.tti.raw.start%22,%22timemark.page.firstScreen.tti.raw.duration%22,%22timemark.page.firstScreen.tti.raw.end%22],%22dimension%22:%22page%22,%22leftValue%22:%22market:index%22,%22rightValue%22:%22market:product%22%7D%7D

## Gauge

Устаревший инструмент для отправки клиентских метрик. Важное отличие от RUM, данные доставляются по стандартному пайплайну Market.Health.

Пайплайн:

Client -> Я.Метрика -> RTMR ... -> Graphite

Пример:

`
one_min.market-front-unified.market_client_timers.v2.white_desktop.requester.splits.human.market_search.firstScreen.metrics.v2.tti_raw.start.quantiles.0_90`

График:

https://market-graphite.yandex-team.ru/?showTarget=one_min.market-front-unified.nginx2.v2.blue_touch.requester.splits.human.any-code.metrics.ttlb.quantiles.0_99&showTarget=one_min.market-front-blue-desktop.timings-dynamic.experiments.test-id.one_min.market-front-blue-desktop.timings-dynamic.experiments.test-id.308651.ALL.0_995&width=776&height=413&from=00%3A00_20200503&until=23%3A59_20210506&target=one_min.market-front-unified.market_client_timers.v2.white_desktop.requester.splits.human.market_search.firstScreen.metrics.v2.tti_raw.start.quantiles.0_90

Логику доставки ищем в market/grafana.

## timers.js

Верхнеуровневый компонент собирающий клиентские метрики.

Список собираемых метрик:

* widget.<id виджета> – время прошедшее с доставки до инициализации
* page.ttfb – время прошедшее с начала запроса (на клиенте) до начала ответа. PerformanceTiming.requestStart/responseStart
* page.loaded – длительность события DOM Loaded. PerformanceTiming.loadEventEnd/Start
* page.domContentLoaded – длительность события DOM ContentLoaded. PerformanceTiming.domContentLoadedEventEnd/Start
* page.firstPaint – время прошедшее от начала запроса до первой отрисовки (first-paint)
* page.firstContentfulPaint – время прошедшее от начала запроса до первой содержательной отрисовки (first-contentful-paint)  

[PerformanceTiming](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceTiming)

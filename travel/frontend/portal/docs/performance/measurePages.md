# Замер страниц

Замер производительности произвольных страниц с помощью lighthouse. [Таск](https://teamcity.yandex-team.ru/buildConfiguration/DataUI_YaTravel_YaTravelFrontend_LighthouseMeasurePages)

## Параметры

Задаются в настройках teamcity билда.

-   `PAGE_URLS` - список замеряемых урлов, разделенных пробелом. Пример - `https://travel-test.yandex.ru/trains/ https://travel-test.yandex.ru/avia/routes/moscow--saint-petersburg/`
-   `ITERATIONS_PER_PAGE` - количество замеров для каждой страницы. Значение по умолчанию - `50`
-   `CONCURRENT_MEASURES` - количество параллельных замеров. Значение по умолчанию - `3`

## Пример результата замеров

```
{
    'https://travel-test.yandex.ru/trains/': {
        score: 52.34,
        fcp: 2851.857974000001,
        lcp: 3799.446377999999,
        speedIndex: 2860.900651330315,
        tti: 7611.930424000002,
        tbt: 1633.5056620000003,
        cls: 0.0002477083333333332,
        maxPotentialFid: 1213.9,
        ttfb: 179.3818,
        mainThreadWork: 3539.9115999999985,
        jsExecutionTime: 2111.0814399999986,
        domSize: 659.1
    },
    'https://travel-test.yandex.ru/avia/routes/moscow--saint-petersburg/': {
        score: 47.54,
        fcp: 3472.1552599999995,
        lcp: 3961.412682,
        speedIndex: 3539.4701199598926,
        tti: 8236.745706000002,
        tbt: 1795.6117089999998,
        cls: 0.00015835774739583332,
        maxPotentialFid: 1763.16,
        ttfb: 455.1121599999999,
        mainThreadWork: 4040.8623999999963,
        jsExecutionTime: 2427.113919999999,
        domSize: 557.62
    }
}
```

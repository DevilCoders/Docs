perf
==
Блок для тонкого профилирования времени выполнения серверного кода.

Оборачивает все блоки, реализованные на технологиях `priv.js` и `bempriv`, в функцию, которая считает время выполнения блока с помощью `process.hrtime`.

Блок работает только под `node.js` и `node-report` или `templar`.

`node-report` нужно запускать с `DEBUG=app:profiling npm start`

`templar` нужно запускать с `PERF=true templar start`

Чтобы выводить результаты логирования в консоль — раскоментируйте строчку в `i-global.priv.js`:
```js
    if (isNodeReportProfileEnabled) {
        // профилирование под node-report // отсылаем данные
        perf.export(data);
        // console.log(perf.getTimes());
    }
```

**Ответственный** — @sbmaxx.

**Пример возвращаемых данных**:

```js
{
    "perf": {
        "time": 18.420298999999996,
        "methods": {
            "_wrapMethod": 1.23128,
            "_wrap": 17.189019
        }
    },
    "i-global": {
        "time": 15.192538999999998,
        "methods": {
            "allowed-flags": 2.497245,
            "variables:validateExpFlag": 0.3919700000000001,
            "variables:parseExpFlag": 0.06174899999999999,
            "variables:getExpFlags": 1.597282,
            "router": 0.087435,
            "variables": 9.252637,
            "counters": 0.188173,
            "params": 1.116048
        }
    },
    "spok": {
        "time": 20.938385999999998,
        "methods": {
            "isDisabled": 0.07875199999999997,
            "getBlacklist": 0.098601,
            "isInBlacklist": 7.590463000000009,
            "overrideBlocks": 13.17057
        }
    },
    "blocks": {
        "time": 360.946241,
        "methods": {
            "i-url": 0.714012,
            "i-cgi": 0.919687,
            "i-cookie": 0.033694,
            "i-seo": 0.605051,
            "cookies": 0.085611,
            "yandex-apps-api": 0.057814,
            "tabs-navigation": 0.125131,
            "suggest2-counter": 0.12655,
            "search2": 1.339251,
            "cbir-logo": 1.041037,
            "head-filter": 1.45873,
            "services-table": 0.044531,
            "service": 1.904667,
            "custom-size": 0.14685,
            "advanced-search": 12.477639,
            "header": 19.358121,
            "presearch-spinner": 0.055717,
            "navigation-controller": 0.027349,
            "categories-index": 0.195149,
            "content_type_index": 10.987817,
            "snippet2": 0.274556,
            "direct_type_fridge": 0.28987,
            "related2": 0.23251,
            "gallery": 0.445999,
            "direct_type_stripe": 0.159129,
            "nps": 0.585231,
            "page-layout": 21.834731,
            "paranja_type_srv": 0.047611,
            "footer": 1.878627,
            "b-mooa": 0.06984,
            "fade": 0.032624,
            "fade_region_main": 0.146589,
            "i-console": 0.05332,
            "timing": 0.200484,
            "b-page": 54.992275,
            "i-response_type_html": 105.582903,
            "i-response": 105.716992
        }
    }
}
```

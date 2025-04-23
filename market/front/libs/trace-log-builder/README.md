# `@yandex-market/trace-log-builder`
Builder for tskv trace logs.

[![npm version](https://badger.yandex-team.ru/npm/@yandex-market/trace-log-builder/version.svg)](https://npm.yandex-team.ru/@yandex-market/trace-log-builder)
[![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/trace-log-builder)](https://oko.yandex-team.ru/pkg/@yandex-market/trace-log-builder)



## Example
```javascript
var TraceLogBuilder = require("trace-log-builder");
var builder = new TraceLogBuilder(
    new Date, 
    LogTraceBuilder.RequestDir.INPUT, 
    "0rkr02kd032dk30d2k203"
    );

builder.setHttpMethod(TraceLogBuilder.HttpMethods.GET);
builder.setSourceModule(TraceLogBuilder.MARKET.FRONT_DESKTOP);
builder.setSourceHost("example.com");
…
var tskv = builder.build();
```

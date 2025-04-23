[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/luster-trace-log)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/luster-trace-log) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=luster-trace-log)](https://oko.yandex-team.ru/pkg/luster-trace-log)

# Luster Trace Log
Luster extension for receiving trace log messages. Plus client logger.

## Example luster configuration for server
```javascript
module.exports = {
    …
    // Расширения для luster
    extensions: {
        'luster-trace-log': {
            markers: { // мапинг маркеров в файлы
                'resource': '/tmp/resource-trace.log'
            },
            socket: '/tmp/luster-trace.sock' // сокет сервера
        }
    }
    …
}
```

## Example default client usage
```
var traceLogger = require("luster-trace-log").Client;
traceLogger.initDefaultLogger("/path/to/socket");

traceLogger.log("resource", "test log message");
```

## Example custom logger client
```
var traceLogger = require("luster-trace-log").Client;
var logger = new traceLogger("/path/to/socket");
logger.log("resource", "test log");
```

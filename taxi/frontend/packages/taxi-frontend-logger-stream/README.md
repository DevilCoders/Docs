# taxi-frontend-logger-stream

Стрим для yandex-logger. Пишет в файл в формате tskv 


## Usage

`npm i --save @yandex-taxi/logger-tskv-stream`

```(js)
const taxiStream = require('@yandex-taxi/logger-tskv-stream');

const logger = require('yandex-logger')({
    name: 'my-app',
    streams: [
        {
            level: 'info',
            stream: taxiStream
        }
    ]
});

logger.error({err, req}, 'Hello world!');
```


https://github.yandex-team.ru/toolbox/yandex-logger

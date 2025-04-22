# cfg [![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/cfg/status.svg)](https://drone.yandex-team.ru/toolbox/cfg) [![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/packages/yandex-cfg&vcs=arc)](https://oko.yandex-team.ru/repo/toolbox/cfg)

Получение конфигурации приложения. Директория `configs` с конфигами ищется от корня приложения (директория с файлом `package.json`).

Окружение выставляется из переменных окружения `CONFIG_ENV` или `NODE_ENV` или `QLOUD_ENVIRONMENT`. Если указанные переменные не определены, то для определения окружения будет использоваться модуль `yandex-environment`

## Install

```
$ npm install --save yandex-cfg
```

## Usage

```js
var cfg = require('yandex-cfg');

cfg.environment;
//=> 'development'

cfg.blackbox.endpoint;
//=> 'blackbox.haze.yandex.net'
```

## License

MIT © [Vsevolod Strukchinsky](http://github.yandex-team.ru/floatdrop)

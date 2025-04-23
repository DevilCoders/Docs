# @yandex-int/yandex-cfg-env 

[![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/yandex-cfg-env/status.svg)](https://drone.yandex-team.ru/toolbox/yandex-cfg-env)

![](http://badger.yandex-team.ru/npm/@yandex-int/yandex-cfg-env/version.svg)
![](http://badger.yandex-team.ru/npm/@yandex-int/yandex-cfg-env/owner.svg?text=owners)

Надстройка над пакетом [```yandex-cfg```](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-cfg) (бывший ```cfg```)

## Install

```npm install --save @yandex-int/yandex-cfg-env```

## Usage

```js
var config = require('@yandex-int/yandex-cfg-env');

config.environment;
//=> 'development'

config.blackbox.endpoint;
//=> 'blackbox.haze.yandex.net'
```

## Dotenv

Если вы используете .env файл (пакет dotenv) - просто добавьте файл configs/env.js с конфигураций, основанной на process.env.* переменных и они (если они будут) будут всегда перезаписывать все, что указано в остальных конфигах.

Например:
```js
module.exports = {
	app: {
		debug: process.env.NODE_DEBUG
	}
};
```

Если запустить NODE_DEBUG=1 npm start с любым окружением, в configs.app.debug всегда будет значение из NODE_DEBUG.

Можно указать чуть более сложное значение:

```js
module.exports = {
	app: {
		debug: parseInt(process.env.NODE_DEBUG, 10) === 1 ? true : undefined
	}
};
```

В такой ситуации, если нет переменной окружения NODE_DEBUG будут использоваться дофолты из default.js или NODE_ENV.js файлов

## Debug

Запуск приложения с инспектированием получившегося конфига:

```
CFG_DEBUG=1 npm start
```

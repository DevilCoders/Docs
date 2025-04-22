# yandex-config [![Build Status](http://drone.haze.yandex.net/api/badge/github.yandex-team.ru/project-stub/yandex-config/status.svg?branch=master&style=flat)](http://drone.haze.yandex.net/github.yandex-team.ru/project-stub/yandex-config)

Обертка над [configs-overload](https://github.com/floatdrop/configs-overload) для загрузки environment-зависимых конфигов.

## Installation

Set your npm registry server to `http://npm.yandex-team.ru` then `npm install yandex-config`

## Usage

```js
var yandexConfig = require('yandex-config');
var config = yandexConfig({ dir: __dirname });
// => {server: {host: 'yandex.ru'}}

config.extend({server: {port: 9090}});
// => {server: {host: 'yandex.ru', port: 9090}}

config.extend('configs/local.js');
// => {server: {host: 'dev.yandex-team.ru', port: 9090}}
```

## API

### yandexConfig(options)

Возвращает объект с конфигами и методом `.extend`

#### options

##### env
Type: String
Default: yandex-environment

Текущее окружение. По умолчанию используется [yandex-environment](https://github.yandex-team.ru/project-stub/yandex-environment), если его нет - то `process.env.NODE_ENV`.

##### default
Type: String
Default: `default`

Окружение по умолчанию, настройки которого будут доопределяться из настроек `env`. То есть файл `configs/default.js` будет доопределен `conifigs/env.js` (где `env` - это текущее окружение, например `testing`).

##### dir
Type: String
Default: `process.cwd()/configs`

Директория с конфигурационными файлами. По умолчанию `path.join(process.cwd(), 'configs')`.

#### extend

Каждый возвращенный объект с конфигами может быть в ручную доопределен методом [`extend(...objects)`](https://github.com/floatdrop/configs-overload#methods).

## Поддержка TypeScript
В файле `index.d.ts` описан неймспейс `YandexConfig`, базовый интерфейс конфига для приложения `Config`, а так же интерфес описывающий опции `Options`, которые можно передать при инициализации конфига.

### Пример настройки конфига на конкретном сервисе
`@types/@yandex-int__yandex-config/index.d.ts`
```typescript
/// <reference types="@yandex-int/yandex-config" />
import { CorsOptions } from 'cors';
import { CsrfOptions } from '@yandex-int/csrf';

declare global {
    namespace YandexConfig {
        interface Config {
            cors: CorsOptions;
            csrf: CsrfOptions;
        }
    }
}
```

`lib/config.ts`
```typescript
/// <reference path="../@types/@yandex-int__yandex-config/index.d.ts" />
import createConfig from '@yandex-int/yandex-config';

export const config = createConfig();
```

Таким образом вы опишите конфиг с двумя обязательными полями `cors` и `csrf` типов `CorsOptions` и `CsrfOptions` соответственно.

И при инициализиции явно укажите что описание интерфеса нужно брать из вашей проектной `@types` директории.

# environment [![Build Status](http://drone.haze.yandex.net/api/badge/github.yandex-team.ru/project-stub/yandex-environment/status.svg?branch=master)](http://drone.haze.yandex.net/github.yandex-team.ru/project-stub/yandex-environment)

This module trys to read `/etc/yandex/environment.type` and return trimmed value inside it. If no such file exist - then `undefined` will be returned.

## Install

Set your npm registry server to `http://npm.yandex-team.ru` then `npm install yandex-environment`

## Example

```js
require('yandex-environment') // development
```

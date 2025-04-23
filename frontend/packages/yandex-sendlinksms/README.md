# yandex-sendlinksms [![Build Status](http://drone.haze.yandex.net/api/badge/github.yandex-team.ru/project-stub/yandex-sendlinksms/status.svg?branch=master)](http://drone.haze.yandex.net/github.yandex-team.ru/project-stub/yandex-sendlinksms)

Promise-based wrapper of /sendlinksms service

## Install

Set your npm registry server to `http://npm.yandex-team.ru` then `npm install yandex-sendlinksms`

## Example

```js
var sms = new SendLinkSms();
// or
var sms = new SendLinkSms('sms.mobile.yandex.net', { timeout: 5000 });

sms.send({
	app: 'maps',
	remote_ip: '87.250.248.242',
	phone_full: '+79999999999',
	lang: 'ru'
}).then();

//or

sms.send({
	app: 'maps',
	remote_ip: '87.250.248.242',
	phone: '9999999',
	code: '999',
	countrycode: '7',
	lang: 'ru'
}).then();
```

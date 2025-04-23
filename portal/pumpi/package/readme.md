# yandex-useragent [![Build Status](http://drone-beta.haze.yandex.net/api/badges/project-stub/yandex-useragent/status.svg)](http://drone-beta.haze.yandex.net/project-stub/yandex-useragent)
[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/yandex-useragent/status.svg)](https://drone.yandex-team.ru/project-stub/yandex-useragent)  
Standalone версия uatraits без зависимости от пакетов. Обновляется по мере необходимости.

## Install

```
$ npm install --save yandex-useragent
```


## Usage

```js
var yandexUseragent = require('yandex-useragent');

yandexUseragent.detect('HTC_Smart_F3188 Mozilla/5.0 (like Gecko) Obigo/Q7');
//=> {isMobile: true, BrowserName: "Obigo", isWAP: true, ...}
```


## API

### yandexUseragent.detect(useragent)

Возвращает объект с полями (подробнее [см. вики](https://beta.wiki.yandex-team.ru/morda/browserdetect/#vsevozmozhnyepoljaiznachenija)):

  - BrowserEngine
  - BrowserEngineVersion
  - BrowserName
  - BrowserShell
  - BrowserShellVersion
  - BrowserVersion
  - GoogleToolBar
  - GoogleToolBarVersion
  - J2ME
  - MailRuAgent
  - MailRuAgentVersion
  - MailRuSputnik
  - MailRuSputnikVersion
  - MultiTouch
  - OSFamily
  - OSName
  - OSVersion
  - PreferMobile
  - Vendor
  - YandexBar
  - YandexBarVersion
  - isBeta
  - isBrowser
  - isEmulator
  - isMobile
  - isRobot
  - isTablet
  - isTouch
  - isWAP
  - x64

#### useragent

*Required*  
Type: `string`

Строка юзер-агента от бразуера.

## Обновление

Чтобы обновить модуль нужно:

> Не забудьте переключиться на npm.yandex-team.ru

 1. `npm install`
 2. `npm run build`
 3. `npm test`
 4. `npm version patch`
 5. `npm publish`

## License

MIT © [Vsevolod Strukchinsky](http://github.com/floatdrop)

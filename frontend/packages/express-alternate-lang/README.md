# Express Alternate Lang [![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/express-alternate-lang/status.svg)](https://drone.yandex-team.ru/toolbox/express-alternate-lang)

![](http://badger.yandex-team.ru/npm/express-alternate-lang/version.svg)
![](http://badger.yandex-team.ru/npm/express-alternate-lang/owner.svg?text=owners)

Мидлвара для express, которая устанавливает в заголовках ответа ссылки 
на альтернативные версии запрошенной страницы на других языках 
или в других регионах. Это помогает роботам определить, какую именно 
версию страницы лучше показать в результатах поиска конкретному пользователю.

## Установка

```
npm install express-alternate-lang --save
```

```js
const expressAlternateLang = require('express-alternate-lang');

app.use(expressAlternateLang());
```

## Ссылки

* Google: https://support.google.com/webmasters/answer/189077?hl=ru
* Yandex: https://yandex.ru/support/webmaster/yandex-indexing/locale-pages.xml
* Языковые коды: https://ru.wiktionary.org/wiki/Викисловарь:ISO_639
* Коды регионов: https://ru.wikipedia.org/wiki/ISO_3166-1

## Конфигурация

### domainsByLang

Объект отношения языков и доменов. На каком домене должен находиться какой язык.

Ключи - язык (или язык-регион) из кодов языков.  
Значения - домен верхнего уровня (tld).

### urlTransformer

Функция, которая модицирует текущий адрес. 

Аргументы:
1. **url** - объект URL текущего адреса https://nodejs.org/docs/latest-v8.x/api/url.html
2. **tld** - домен, пришедший из конфига domainsByLang
3. **lang** - язык, соответсвтующий домену из конфига domainsByLang

## Использование 

### Дефолтная логика:

```js
const config = {
    domainsByLang: {
        ru: 'ru',
        en: 'com',
        be: 'by',
        tr: 'com.tr',
        uk: 'com.ua'
    }
};

app.use(require('express-alternate-lang')(config));

app.get('*', (req, res) => res.send());
```

```$ curl -X GET -I http://localhost/ -H 'Host: example.org'

HTTP/1.1 200 OK
Link: <http://example.ru/>; rel="alternate"; hreflang="ru"
Link: <http://example.com/>; rel="alternate"; hreflang="en"
Link: <http://example.by/>; rel="alternate"; hreflang="by"
Link: <http://example.com.tr/>; rel="alternate"; hreflang="tr"
Link: <http://example.com.ua/>; rel="alternate"; hreflang="uk"
```

### Своя логика:

```js
const config = {
    domainsByLang: {
        ru: 'ru',
        en: 'com',
        be: 'by',
        tr: 'com.tr',
        uk: 'com.ua'
    },
    urlTransformer: (url, tld, lang) => {
        url.pathname = `${tld}/${url.pathname}`;
        return url;
    }
};

app.use(require('express-alternate-lang')(config));

app.get('*', (req, res) => res.send());
```

```$ curl -I http://localhost/ -H 'Host: example.org'

HTTP/1.1 200 OK
Link: <http://example.org/ru/?lang=ru>; rel="alternate"; hreflang="ru"
Link: <http://example.org/com/?lang=en>; rel="alternate"; hreflang="en"
Link: <http://example.org/by/?lang=by>; rel="alternate"; hreflang="by"
Link: <http://example.org/com.tr/?lang=tr>; rel="alternate"; hreflang="tr"
Link: <http://example.org/com.ua/?lang=uk>; rel="alternate"; hreflang="uk"
```

### Пример с "x-default":

```js
const config = {
    domainsByLang: {
        ru: 'ru',
        en: 'com',
        'x-default': 'org'
    }
};

app.use(require('express-alternate-lang')(config));

app.get('*', (req, res) => res.send());
```

```$ curl -I http://localhost/ -H 'Host: example.org'

HTTP/1.1 200 OK
Link: <http://example.ru/>; rel="alternate"; hreflang="ru"
Link: <http://example.com/>; rel="alternate"; hreflang="en"
Link: <http://example.org/>; rel="alternate"; hreflang="x-default"
```

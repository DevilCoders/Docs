# Content Security Policy

* [О технологии CSP](#csp-about)
  * [Директивы](#directives)
  * [Источники](#sources)
  * [Специальные значения nonce и hash](#nonce)
  * [Примеры установки](#example)
  * [Поддержка в браузерах](#bro)
  * [Полезные ссылки](#links)
* [Политика по умолчанию в islands](#csp-default)
* [Подготовка сервиса к внедрению CSP](#csp-pre)
* [Подключение политики по умолчанию](#add-csp)
* [Переопределение политики по умолчанию](#csp-redefinition)

<a name="csp-about"></a>
## О технологии CSP

**Content Security Policy** (CSP или политика безопасности контента) — новый [W3C](http://w3c.org.ru/?p=3280)-стандарт для повышения безопасности веб-приложений. Текущая версия стандарта [Content Security Policy Level 2](http://www.w3.org/TR/CSP/) (CSP2) находится в статусе Candidate Recommendation.

CSP позволяет разработчикам явно определить разрешенный (белый) список источников, откуда могут загружаться различные ресурсы страницы (скрипты, изображения, стили, шрифты и т. п.). Поддержка политики на стороне браузера помогает обнаружить и предотвратить некоторые виды атак, в том числе XSS.

Разрешенный список источников объявляется в HTTP-заголовках, которые сервер отправляет браузеру:

* `Content-Security-Policy` – браузер блокирует все ресурсы, которые не соответствуют политике безопасности.
* `Content-Security-Policy-Report-Only` – браузер проверяет все ресурсы, но не блокирует их, а только сообщает о нарушениях в форме JSON-отчета (режим отладки).

В CSP2 появилась возможность задавать политики с помощью [метатега](https://w3c.github.io/webappsec/specs/CSP2/#delivery-html-meta-element) (поддерживается в браузерах на базе Chromium: Yandex.Browser, Chrome, Chromium и Safari Version 7.1.4).

---
**NB** В библиотеках `islands-*` CSP объявляется в метатеге.
Режим отладки в метатеге не доступен, так как директива [report-uri игнорируется в метатеге](http://www.w3.org/TR/CSP2/#directive-report-uri). Для отладки рекомендуется продублировать политику в HTTP-заголовке.

---

Политика состоит из списка директив. Директива — часть политики, контролирующая определенный ресурс браузера (стили, изображения и т. д.). Директивы отделяются символом `;`. Все источники одного типа должны быть перечислены в одной директиве.

<a name="directives"></a>
### Директивы
Набор директив в [текущей](http://www.w3.org/TR/CSP/) версии стандарта:

| Директива   | Назначение |
| ----------- | ---------- |
| default-src | Список разрешенных источников, который используется в качестве значения для не заданных явно директив. [Директивы](http://www.w3.org/TR/CSP2/#directive-default-src), для которых могут быть определены значения по умолчанию в `default-src`. <br> *Обратите внимание, что специализированные директивы для соответствующего ресурса (например, `script-src`) не наследуют, а полностью переопределяют директиву `default-src`.* |
| script-src  | Разрешенные источники для загрузки и выполнения js-скриптов (значения для атрибута `src` тега `<script>)`. |
| style-src | Разрешенные источники для загрузки CSS-стилей. |
| img-src | Разрешенные источники для загрузки изображений. |
| frame-src | Разрешенные источники для загрузки фреймов. <br> [Директива](http://www.w3.org/TR/CSP2/#directive-frame-src) в CSP2 отмечена устаревшей в пользу `child-src`, но браузеры пока поддерживают только `frame-src`. |
| object-src  | Разрешенные источники для загрузки Flash-подобных плагинов. |
| media-src   | Разрешенные источники для загрузки аудио и видео. |
| font-src | Разрешенные источники для загрузки шрифтов. |
| connect-src | Ограничивает источники, к которым можно подключаться с помощью: `XMLHttpRequest`, `WebSocket`, `EventSource`, атрибута `ping` в элементе `<a>`, `sendBeacon(url)`. |
| report-uri | URL, на который браузер отправляет JSON-отчет о нарушениях политики.   Отправка выполняется методом POST. Директива игнорируется в метатеге.|
|sandbox | Ограничения на действия, которые могут выполняться на странице, а не на ресурсы, которые страница может загружать. Если директива задана, то страница будет рассматриваться так, будто она загружена внутри `iframe` с атрибутом `sandbox`. С помощью этой директивы можно добиться различных эффектов, например, присвоить странице уникальный источник, предотвратить отправку форм и т. п. Директива игнорируется в метатеге.|

[Полный список директив CSP2](https://w3c.github.io/webappsec/specs/content-security-policy/#directives).

<a name="sources"></a>
### Источники

Помимо URL в качестве источника могут быть указаны следующие ключевые слова (обязательно в одинарных кавычках):

| Ключевое слово |	Назначение |
| -------------- | ---------- |
| 'self' | Соответствует текущему источнику (протокол, хост, порт), но не его поддоменам. |
| 'none' | Запрещает все. |
| 'unsafe-inline' | Разрешает использовать инлайновые JavaScript и CSS. Используется только в директивах `script-src` и `style-src`.<br> По возможности старайтесь не использовать данное ключевое слово, так как это напрямую разрешает исполнять любой инлайн-JavaScript на странице. Что может стать источником уязвимостей, допускающих XSS-атаки.|
| 'unsafe-eval' | Разрешает выполнение JavaScript-кода с помощью функций `eval`, `setTimeout` и `setInterval`. Используется только в `script-src`. |

Список источников в каждой директиве можно гибко настроить:

* Задать в источнике схему (`data:`, `https:`) (например, `default-src 'self' data: example.com; img-src: https://myimage.com`).
* Использовать только диапазон хостов (например, `example.com` будет соответствовать источнику с любой схемой или портом для указанного хоста).
* Указать полностью URI (`https://example.com:443`, будет соответствовать только HTTPS, только `example.com`, и только порту 443).
* Использовать маски, но только для схемы, порта или крайней левой позиции имени хоста: `*://*.example.com:*` соответствует всем поддоменам `example.com` (но не самому `example.com`), с любой схемой и портом.

В случае, если политика указана и в HTTP-заголовке, и в метатеге – приоритет у политики HTTP-заголовка с сервера. Если в метатеге указана одноименная директива, она игнорируется. Если в метатеге указана директива, которой нет в заголовке сервера – она применяется. Если в серверной политике указано `default-src`, то директивы метатега игнорируются.

<a name="nonce"></a>
### Специальные значения nonce и hash

В CSP2 добавлена возможность блокировать не все инлайновые скрипты/стили, а только неизвестные, для директив `script-src` и `style-src` существуют специальные временные значения `nonce` и `hash`. Они позволяют задать уникальное значение (ключ) для разрешенных скриптов и стилей.


#### nonce

Специальное значение `nonce` позволяет задать уникальный ключ `$RANDOM`.

`nonce-$RANDOM` разрешает использовать инлайновые JavaScript и CSS, у которых атрибут `nonce` равен `$RANDOM` (случайная последовательность символов передаваемых в заголовке, для подписи доверенного инлайн-кода).  Значение `nonce-$RANDOM` будет добавлено к директивам `script-src` и `style-src` и их содержимое не заблокируется даже при отсутствии ключевого слова `unsafe-inline`.

Если есть `unsafe-inline` и `nonce`, то `nonce` выключает `unsafe-inline` и
выполняются только те инлайн-скрипты, которые подписаны атрибутом `nonce` с той же последовательностью символов.

Пример генерации значения `nonce` для Node.js:

```javascript
/**
 * Генерация уникального ключа для Content Security Policy
 */
CspSafeMixin.prototype.generateNonceId = function() {
    return crypto.randomBytes(16).toString('base64');
};
```

Например, если в директиве указано:

```javascript
script-src: 'nonce-Nc3n83cnSAd3wc3Sasdfn939hc3'; style-src: 'nonce-Nc3n83cnSAd3wc3Sasdfn939hc3';
```

то будут разрешены:

```html
<script nonce="Nc3n83cnSAd3wc3Sasdfn939hc3">
alert("Allowed because nonce is valid.");
</script>
<style nonce="Nc3n83cnSAd3wc3Sasdfn939hc3">
    .inline {}
</style>
```

*Обратите внимание, `nonce` не работает для подключения внешних стилей через тег `link`*.

То есть следующий код не выполнится:

```html
<link rel="stylesheet" nonce="Nc3n83cnSAd3wc3Sasdfn939hc3" href="http://mysite.ru/mysite.css"">
```

#### hash

`sha256-$HASH`, где `$HASH` – [sha256 base64](https://ru.wikipedia.org/wiki/SHA-2) хеш от содержимого для скриптов в `<script>`, для стилей –  от содержимого `<style>`.

Например, если в директиве указано:

```javascript
script-src: 'sha256-D/KBQFzg9Qy1HzLAR8QcGAvMgwwhzLaiRBk+V4pPe6A'; style-src: 'sha256-FbPRQ6DSOl2/d0Hyh+xNkRMdj3BSf3pjO3Lm7zIIvJQ';
```
то будут разрешены:

```html
<script>alert("Allowed because hash is valid.");</script>
<style>.inline { background: red; }</style>
```
Значений `'sha256-$HASH'` может быть несколько, для каждого скрипта/стиля.

[Онлайн-утилита](http://approsto.com/sha-generator/) для вычисления `SHA`.


<a name="example"></a>
### Примеры установки CSP

**HTTP-заголовок**

```js
Content-Security-Policy: default-src 'none'
```

```js
Content-Security-Policy: default-src 'self'; script-src yastatic.net  yandex.ru 'self' 'unsafe-inline' 'unsafe-eval'; style-src yastatic.net 'self' 'unsafe-inline'; img-src yastatic.net data: avatars.yandex.net clck.yandex.ru 'self'; connect-src mc.yandex.ru 'self'
```

**Метатег**

```js
<meta http-equiv="Content-Security-Policy" content="default-src 'none';" />
```

```js
<meta http-equiv="Content-Security-Policy" content= "default-src 'self'; script-src yastatic.net  yandex.ru 'self' 'unsafe-inline' 'unsafe-eval'; style-src yastatic.net 'self' 'unsafe-inline'; img-src yastatic.net data: avatars.yandex.net clck.yandex.ru 'self'; connect-src mc.yandex.ru 'self';" />
```

<a name="bro"></a>
### Поддержка CSP в браузерах

CSP1 поддерживают все популярные [браузеры](http://caniuse.com/#search=csp):

* Chrome 25+
* Firefox 23+
* Opera 15+
* Яндекс.Браузер
* IE поддерживает CSP только в [preview release](https://status.modern.ie/contentsecuritypolicy) (март 2015, возможно в течение года ситуация изменится).

*Обратите внимание, директивы добавленные в CSP2, пока частично поддерживаются [браузерами](#bro)*.

<a name="links"></a>
### Полезные ссылки о CSP

* [Спецификация W3C](http://www.w3.org/TR/CSP2/)
* [Подробное описание директив CSP](http://www.w3.org/TR/CSP2/#directives)
* [Описание отличий CSP 2.0 от CSP 1.0](https://w3c.github.io/webappsec/specs/content-security-policy/#changes-from-level-1) (есть обратно несовместимые изменения)

<a name="csp-default"></a>
## Политика по умолчанию в библиотеках islands

Политика по умолчанию в `islands` – это базовая политика, общая для всех сервисов, которой будет достаточно большинству проектов.

Подключается политика с помощью метатега `<meta http-equiv="Content-Security-Policy" content="[POLICY GOES HERE]">` в шаблоне блока [b-page](https://github.yandex-team.ru/lego/islands-romochka/blob/dev/common.blocks/b-page/b-page.ru.md) на уровне `common` библиотеки [islands-romochka](https://github.yandex-team.ru/lego/islands-romochka).

Настройки политики по умолчанию содержатся в [документации блока b-page](https://github.yandex-team.ru/lego/islands-romochka/blob/dev/common.blocks/b-page/b-page.ru.md#default-csp-policy). На сервисе политику по умолчанию можно самостоятельно [подключить](#add-csp) или [переопределить](#csp-redefinition) несколькими способами.

<a name="csp-pre"></a>
## Подготовка сервиса к внедрению CSP

[Подробно о подготовке сервиса к внедрению CSP](https://beta.wiki.yandex-team.ru/product-security/csp).

Прежде чем включить на сервисе CSP, важно самостоятельно проверить приложение на наличие нарушений и исправить их.

Проверка выполняется в режиме отладки, с помощью заголовка `Content-Security-Policy-Report-Only`. Браузер отправит [JSON-отчет](https://wiki.mozilla.org/index.php?title=Security/CSP/Spec&oldid=217177#Report-Only_mode) о найденных нарушениях политики на URL, указанный в директиве `report-uri`.

---
**NB** Для режима отладки продублируйте политику в HTTP-заголовок.

---

Поскольку в метатеге нельзя включить директиву [report-uri](http://www.w3.org/TR/CSP2/#directive-report-uri), для отладки политики воспользуйтесь одним из альтернативных способов:

* Включить директиву `report-uri` в НТТP-заголовке сервера и проверить отчеты о нарушениях политики (способ включения зависит от [используемого сервера](#server)) c помощью централизованного сервиса отчетов Яндекса для CSP ([на стадии разработки](https://st.yandex-team.ru/MARTY-188)).
* Проверить в консоли браузера, наряду с остальными заголовками.

Кроме того, существует несколько OpenSource-инструментов для сбора и анализа отчетов браузеров:

* [csp-reporter](https://github.com/yandex/csp-reporter) – утилита для генерации отчетов CSP.
* [csp-tester](https://github.com/yandex/csp-tester) – расширение для Chromium-браузера (Yandex.Browser, Chrome, Chromium), которое позволяет добавлять заголовки на страницу и упрощает отладку CSP.

<a name="server"></a>
Примеры конфигурации веб-сервера с политикой по умолчанию:

**nginx**

```nginx
server {
    listen 80;
    location / {
        # http://nginx.org/ru/docs/http/ngx_http_headers_module.html
        add_header Content-Security-Policy "default-src 'self' yastatic.net; script-src 'self' yastatic.net yandex.ru mc.yandex.ru social.yandex.ru export.yandex.ru suggest.yandex.ru notifications.yandex.ru suggest-slovari.yandex.ru suggest-market.yandex.ru; style-src 'self' yastatic.net 'unsafe-inline'; img-src 'self' yastatic.net data: awaps.yandex.ru kiks.yandex.ru mc.yandex.ru yabs.yandex.ru avatars.yandex.net www.tns-counter.ru clck.yandex.ru; frame-src 'self' yastatic.net awaps.yandex.ru pass.yandex.ru legal.yandex.ru notifications.yandex.ru; connect-src 'self' mc.yandex.ru;";
    }
}
```

**nodejs**

```js
http.createServer(function (req, res) {
    res.writeHead(200,
    {
        'Content-Security-Policy': "default-src 'self' yastatic.net; script-src 'self' yastatic.net yandex.ru mc.yandex.ru social.yandex.ru export.yandex.ru suggest.yandex.ru notifications.yandex.ru suggest-slovari.yandex.ru suggest-market.yandex.ru; style-src 'self' yastatic.net 'unsafe-inline'; img-src 'self' yastatic.net data: awaps.yandex.ru kiks.yandex.ru mc.yandex.ru yabs.yandex.ru avatars.yandex.net www.tns-counter.ru clck.yandex.ru; frame-src 'self' yastatic.net awaps.yandex.ru pass.yandex.ru legal.yandex.ru notifications.yandex.ru; connect-src 'self' mc.yandex.ru;"
    });

});
```

**expressjs**

```js
var express = require('express');
var app = express();

app.use(function(req, res, next) {
    res.setHeader("Content-Security-Policy",
        "default-src 'self' yastatic.net; script-src 'self' yastatic.net yandex.ru mc.yandex.ru social.yandex.ru export.yandex.ru suggest.yandex.ru notifications.yandex.ru suggest-slovari.yandex.ru suggest-market.yandex.ru;style-src 'self' yastatic.net 'unsafe-inline'; img-src 'self' yastatic.net data: awaps.yandex.ru kiks.yandex.ru mc.yandex.ru yabs.yandex.ru avatars.yandex.net www.tns-counter.ru clck.yandex.ru; frame-src 'self' yastatic.net awaps.yandex.ru pass.yandex.ru legal.yandex.ru notifications.yandex.ru; connect-src 'self' mc.yandex.ru;"
    );
    return next();
});
```

<a name="add-csp"></a>
## Подключение политики по умолчанию

Политика безопасности подключается несколькими способами, которые различаются областью применения в пределах страницы или всего сервиса.

### Локальное подключение

Подключить политику только для отдельной страницы сервиса можно в поле `csp` BEMJSON блока. Рекомендуемый способ.

```javascript
{
    block: 'b-page',
    csp: true
}
```

Метатег с CSP будет расположен сразу после тега `<html>`. Политика применяется ко всем
ресурсам страницы расположенным в `<head>`(как внешним, подключенным по `<script src="example.com">`, так и добавляемым в самом документе).

Существует дополнительная возможность подключить политику в элементе блока `csp` в поле `head`. В этом случае, метатег будет последним элементом в `<head>`.

---
**NB** Этот способ применять не рекомендуется, так как код загружаемый до метатега CSP не проверяется на соответствие политике безопасности. Например, данные плагинов для браузеров.

---

```javascript
{
    block: 'b-page',
    head: [
        { elem: 'csp': csp: true }
    ]
}
```

### Глобальное подключение

Подключить политику для всего сервиса можно переопределив шаблон BEMHTML/BH элемента блока `csp`.

**BEMHTML**

```javascript
block b-page, elem csp, default: {
    this.ctx.policies = true;
    applyNext();
}
```

**BH**

```javascript
module.exports = function(bh) {
    bh.match('b-page__csp', function(ctx) {
        ctx.param('policies', true);
    });
};
```


---
**NB** Обратите внимание, что для подключения политики любым из способов, нужно добавить зависимость в блок `b-page` от элемента `csp`.

---
```js
({
    shouldDeps: { elems: ['csp'] }
})
```

В блоке `b-page` реализована возможность добавлять на страницу инлайн-скрипты и стили с атрибутом [nonce](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/b-page/b-page.ru.md#%D0%9F%D0%B5%D1%80%D0%B5%D0%B4%D0%B0%D1%87%D0%B0-nonce).


<a name="csp-redefinition"></a>

## Переопределение политики

---
**NB** Если вы планируете переопределять политику по умолчанию, проконсультируйтесь со <a href="mail:product-security@yandex-team.ru">службой безопасности</a>.

---

Способы переопределения политики аналогичны перечисленным в разделе [Подключение политики](#add-csp). Но предварительно нужно указать разрешенные источники в списке требуемых директив.

Переопределять можно как [директивы](https://github.yandex-team.ru/lego/islands-romochka/blob/dev/common.blocks/b-page/b-page.ru.md#default-csp-policy) заданные в политике по умолчанию, так и любые из списка [директив](http://www.w3.org/TR/CSP2/#directive
), реализованные в CSP2.

Следует помнить, что директивы `report-uri` и `sandbox` нельзя задать через метатег (согласно спецификации, в метатеге они игнорируются).


### Локальное переопределение

В поле `csp` BEMJSON блока. Значение каждой директивы – массив разрешенных источников. Рекомендуемый способ.

```javacsript
({
    block: 'b-page',
    csp: {
        policies: {
            'script-src': [
                'from-bemjson.net',
                'example.com'
            ],
            style-src': [
                'mystyle.net'
            ]
        }
    }
});
```

Список источников в каждой директиве можно [гибко настроить](https://beta.lego.yandex-team.ru/guidelines/security-policy/#Источники).

```javacsript
({
    block: 'b-page',
    csp: {
        policies: {
            'script-src': [
                'from-bemjson.net',
                'example.com'
            ],
            style-src': [
                'self',
                'data: example.com'
            ]
        }
    }
});
```

Переопределение политики в элементе блока `csp` в поле  блока `head`. Не рекомендуется использовать (способ небезопасный).

 ```javascript
 ({
    block: 'b-page',
    head: [
        {
            elem: 'csp',
            policies: {
                'script-src': [
                    'from-bemjson.net',
                    'example.com'
                ],
                'style-src': [
                    'mystyle.net'
                ]
            }
        }
    ]
});
 ```

### Глобальное переопределение

Выполняется переопределением шаблонов элемента блока `csp`.

**BEMHTML**

```javascript
block b-page, elem csp, default: {
    this.ctx.policies = {'script-src': ['test-from-bemhtml.net']};
    applyNext();
}
```

**BH**

```javascript
module.exports = function(bh) {
    bh.match('b-page__csp', function(ctx) {
        ctx.param('policies', {'script-src': ['test-from-bemhtml.net']});
    });
};
```

# Набор CSP-правил для сервисов Яндекса

![](https://badger.yandex-team.ru/npm/@yandex-int/csp-presets-pack/version.svg)
![](https://badger.yandex-team.ru/npm/@yandex-int/csp-presets-pack/owner.svg)

## Как установить?

```bash
npm install @yandex-int/csp-presets-pack --registry=http://npm.yandex-team.ru/ --save
```

или

```bash
yarn add @yandex-int/csp-presets-pack --registry=http://npm.yandex-team.ru/
```

## Как использовать?

В configs/*.js подключаем модуль:

```js
const csp = require('@yandex-int/csp-presets-pack');
```

или

```js
import csp from '@yandex-int/csp-presets-pack';
```

и далее в нужном месте используем:

```js
csp: {
    presets: [
        csp.yaStatic(),
        csp.s3('testing', 'bucket_name'),
        csp.metrika(),
        csp.forms(),
        csp.resizer('testing', ['img-src'])
    ]
},
```

## API

Каждый сервис является методом, в который можно передавать аргументы:

* **env** - Принимается окружение. В основном это testing или нет. Некоторые сервисы не имеют окружений. Там где оно важно, по умолчанию - `production`.
* **options** - зависящие от сервиса опции подключения. Например, у S3 это имя бакета
* **rules** - массив правил, в которых нужно использовать этот сервис, если он отличается от стандартного. Некоторые сервисы не используют этот аргумент, например, Метрика.

```js
csp.service(env, options, rules);
```

```js
csp.service(env, rules);
```

```js
csp.service(env);
```

Некоторые сервисы работают независимо от окружения (например yastatic.net)

```js
csp.service();
```

или же все таки принимать правила

```js
csp.service(rules);
```

## Доступные сервисы:

### yaStatic

Для подключения файлов, хранящихся на yastatic.net

```js
presets: [
    csp.yaStatic(sources[])
]
```

* **source** - по умолчанию изображения, медиа, скрипты, шрифты и стили

Первый аргумент (окружение) роли не играет.

В качестве правил, по умолчанию используются:
* script-src
* style-src
* font-src
* img-src
* media-src

### s3

Понадобится в случае подключения файлов, хранящихся на S3 Яндекса

```js
presets: [
    csp.s3(env, bucketName, source[])
]
```

* **env** - окружение: для production - bucket.s3.mds.yandex.net и bucket.s3.yandex.net, для всего остального - bucket.s3.mdst.yandex.net
* **bucketName** - имя бакета
* **source** - по умолчанию изображения, медиа, скрипты, шрифты и стили

### avatars

Если вы используете аватарницу:

```js
presets: [
    csp.avatars(env)
]
```

* **env** - окружение: для production - avatars.mds.yandex.net, для всего остального - avatars.mdst.yandex.net

### metrika

Устанавливает значения в соответствии с рекомендациями https://wiki.yandex-team.ru/product-security/csp/metrika/

```js
presets: [
    csp.metrika(tlds)
]
```

* **tlds** - массив tld, на которые может ходить метрика. По умолчанию используется полный список всех возможных доменов, включая экзотические .com.il и подобные.

### appmetrika

Разрешает подключения метрики к серверу appmetrika на портах 29009, 29010 и 30102, 30103

```js
presets: [
    csp.appmetrika({ byIp: true, byDomain: true})
]
```

* **config**
** **byIp** - разрешать подключения к 127.0.0.1 по соответствующим портам
** **byDomain** - разрешать подключения к yandexmetrika.com по соответствующим портам

Подробнее тут: https://st.yandex-team.ru/SERP-65110

### maps

```js
presets: [
    csp.maps()
]
```

Не принимает параметров. Устанавливает значения в соответствии с рекомендациями https://wiki.yandex-team.ru/maps/api/csp

### resizer

```js
presets: [
    csp.resizer(env)
]
```

* **env** - окружение: для production использует resize.yandex.net, для всего остального - resize.rs.yandex.net

### forms

```js
presets: [
    csp.forms()
]
```

### passport

```js
presets: [
    csp.passport(env)
]
```

* **env** - окружение: для не production используется префикс `-test` в некоторых случаях

### browser-updater

```js
presets: [
    csp.browserUpdater()
]
```

### direct

```js
presets: [
    csp.direct()
]
```

Не принимает параметров. Устанавливает значения в соответствии с рекомендациями https://wiki.yandex-team.ru/pcode/csp/#rekomenduemajakonfiguracijacsp

NB: Пресет включает `unsafe-inline` (иначе реклама не будет работать), но не включает `nonce-`. Это ответственность вашего сервиса.

### tns

Для подключения счетчика **www.tns-counter.ru**. Содержит только правила img-src в силу запрета загрузки 3rd-party скриптов.

```js
presets: [
    csp.tns()
]
```

### statface

```js
presets: [
    csp.statface(tlds)
]
```

* **tlds** - массив tld, на которые может ходить statface. По умолчанию используется полный список всех возможных доменов.

### gemius

Для подключения счетчика gemius. Содержит только правила img-src в силу запрета загрузки 3rd-party скриптов.

```js
presets: [
    csp.gemius(tlds)
]
```

* **tlds** - массив tld, на которые может ходить gemius. Устанавливает значения по умолчанию в соответствии с доступными странами https://lego.yandex-team.ru/libs/islands/v4.9.0/desktop/b-statcounter/#elems-gemius

### butterfly

```js:
presets: [
    csp.butterfly(exps)
]
```

* **exps** - массив адресов ручек для запросов с экспериментами. По умолчанию используется полный список 'ya.ru' и 'ecoo.n.yandex-team.ru'

### adsdk

Содержит правила, необходимые для работы [рекламного плеера Яндекса](https://wiki.yandex-team.ru/video-ads-sdk/)

```js
presets: [
    csp.adsdk()
]
```

### player

Содержит правила, необходимые для работы видео плеера Яндекса при подключении его напрямую на страницу сервиса (без iframe),
подробнее: [метод вставки через js-api](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/contribs/video-player/VH.md)

При вставке плеера через iframe ([пример](https://frontend.vh.yandex.ru/player/4393e520096a095b94559f0939bc2170?autoplay=0), 
[документация](https://yandex.ru/support/video-hosting/embed-code.html)) данный пресет не требуется.

```js
presets: [
    csp.player()
]
```

## Базовые источники данных:

### none

Для запрещения всего (используется в default-src)

```js
presets: [
    csp.none(sources[])
]
```

* **env** - окружение не используется
* **source** - по умолчанию default-src

### self

Для подключения ресурсов с текущего домена

```js
presets: [
    csp.self(sources[])
]
```

* **env** - окружение не используется
* **source** - по умолчанию для скриптов, стилей, медиа, шрифтов и изображения

### inline

Для разрешения небезопасного исполнения скриптов и стилей из атрибутов

```js
presets: [
    csp.inline(sources[])
]
```

* **env** - окружение не используется
* **source** - по умолчанию для скриптов и стилей

### eval

Для разрешения небезопасного исполнения скриптов

```js
presets: [
    csp.eval(sources[])
]
```

* **env** - окружение не используется
* **source** - по умолчанию только для скриптов

### nonce

Для использования скриптов на странице, одобряемых через nonde

```js
presets: [
    csp.nonce(sources[])
]
```

* **env** - окружение не используется
* **source** - по умолчанию только для скриптов

### data

Для подключения изображений из 'data:' в стилях

```js
presets: [
    csp.data(sources[])
]
```

* **env** - окружение не используется
* **source** - по умолчанию только для изображений

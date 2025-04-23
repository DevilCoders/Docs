# express-bundle-response [![Build Status](http://drone.haze.yandex.net/api/badge/github.yandex-team.ru/project-stub/express-bundle-response/status.svg?branch=master&style=flat)](http://drone.haze.yandex.net/github.yandex-team.ru/project-stub/express-bundle-response)

Миддлвара добавляющая `bundle.render` (и методы хелперы из [bundle-typer](https://github.yandex-team.ru/project-stub/bundle-typer)) в объекте response.

Кратко принцип работы:

 1. Миддлвара определяет тип бандла и язык по функции [detect](https://github.yandex-team.ru/project-stub/express-bundle-response#detect) __при ее вызове__.
 1. В объекте response создается свойство `bundle`, которое можно доконфигурировать в контроллере (см Usage).

## Usage

```js
var app = require('express')();
var path = require('path');

app.use(require('express-bundle-response')());

app.get('/', function (req, res) {
    res.bundle.render('index');
});

app.get('/custom', function (req, res) {
    res.bundle
        .type('touch', req.uatraits.isMobile)
        .render('index');
});

app.get('/en', function (req, res) {
    res.bundle
        .lang('en')
        .render('index');
});

app.listen(8000);
```

## API

### expressBundleResponse([options])

Возвращает миддлвару, которая добавляет в `response` поле `bundle`.

#### options

###### block
Type: `String`
Default: `page`

Имя блока, которое будет передано в `exec` из priv файла первым агрументом.

###### data
Type: `Object`

ОБъект, который будет передан в `exec` функцию из priv файла вторым аргументом.

###### lang
Type: `String`
Default: `ru`

Загружаемый язык. См. [bem-bundle#lang](https://github.yandex-team.ru/project-stub/bem-bundle#lang).

###### cwd
Type: `String`
Default: `static`

Директория, в которой должен находиться бандл `bundleName`.

###### dev
Type: `Boolean`
Default: `false`

Сбрасывать ли кеш `require` перед загрузкой.

###### templateExt
Type: `String`
Default: `bemhtml.js`

Расширение файла с шаблонами (`index.{templateExt}`).

###### typeExt
Type: `String`
Default: `.bundle`

Постфикс директории с бандлами (например `desktop{typeExt}` или `touch{typeExt}`).

###### detect
Type: `Function`

Функция, которая определяет тип и язык бандла. По умолчанию:

```js
function detect(bundle, req) {
    bundle
        .lang((req.langdetect && req.langdetect.id) || this.lang) // this указывает на options
        .type('desktop')
        .type('mobile', req.uatraits && req.uatraits.isMobile)
        .type('touch', req.uatraits && (req.uatraits.MultiTouch || req.uatraits.isTouch));
}
```

Это поведение можно переопределить глобально вот так:

```js
var bundleResponse = require('express-bundle-response')

bundleResponse({
    detect: function (bundle, req) {
        bundle.type('desktop');
    }
});
```

Или доопределить локально в контроллере:

```js
app.get('/en', function (req, res) {
    res.bundle
        .lang('en')
        .render('index');
});
```

## Benchmarks

```bash
$ npm i matcha -g
$ matcha

                      benchmark
          120,352 op/s » render
           46,811 op/s » direct render call
          372,144 op/s » middleware
          776,684 op/s » baseline


  Suites:  1
  Benches: 4
  Elapsed: 3,518.49 ms
```

# bundle-typer [![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/bundle-typer/status.svg)](https://drone.yandex-team.ru/toolbox/bundle-typer)

![](https://badger.yandex-team.ru/npm/bundle-typer/version.svg)
![](https://badger.yandex-team.ru/npm/bundle-typer/owner.svg)

Интерфейс для задания языка, типа бандла и рендеринга его.

## Usage

```js
var app = require('express')();
var path = require('path');

var bundle = require('bundle-typer');
var opts = {
    cwd: '../static',
    dev: true
};

app.get('/', function (req, res) {
    bundle(opts)
        .lang(req.langdetect.id || 'ru')
        .type('desktop')
        .type('mobile', req.uatraits.isMobile)
        .type('touch', req.uatraits.MultiTouch || req.uatraits.isTouch)
        .render('index', { data: {}, name: bundle.name, type: bundle._type }, function (err, html) {
            if (err) { return res.emit('error', err); }
            res.send(html);
        });
});

app.listen(8000);
```

## API

### BundleTyper([options])

Создает объект BundleTyper.

### options

> Все опции из [toolbox-bem-bundle](https://github.yandex-team.ru/toolbox/toolbox-bem-bundle#options)

###### typeExt  
Type: `String`  
Default: `.bundle`

Постфикс директории с бандлами (например `desktop{typeExt}` или `touch{typeExt}`).

###### ignorePriv  
Type: `Boolean`  
Default: `false`

Игнорировать ли `priv.js` файл из Bundle.

### BundleTyper методы

#### lang(language)

Устанавливает язык бандла. Влияет на название priv файла (например `index.priv.ru.js`).

Возвращает BundleTyper.

#### type(name, [flag])

Устанавливает тип бандла. Влияет на путь к бандлу. Если установлен, то бандл будет загржаться из `[type].bundles/[bundleName]`.

###### flag

 * Если `flag !== true` - то тип не будет установлен.
 * Если `flag` опущен - то тип __будет__ установлен.

Возвращает BundleTyper.

#### render(bundleName, [data], callback)

Запускает рендер бандла с опциональными данными из `data`. По окончанию будет вызван `callback`.

#### get(bundleName, [opts])

Возвращает бандл. (См. [toolbox-bem-bundle](https://github.yandex-team.ru/toolbox/toolbox-bem-bundle))

## Related

 * http://strongloop.com/strongblog/bypassing-express-view-rendering-for-speed-and-modularity/

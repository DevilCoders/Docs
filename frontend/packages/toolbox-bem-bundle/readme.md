# toolbox-bem-bundle

![](https://badger.yandex-team.ru/npm/toolbox-bem-bundle/version.svg)
![](https://badger.yandex-team.ru/npm/toolbox-bem-bundle/owner.svg)

API для работы с бандлами. Загружает priv и bemhtml файлы и прочее.

## Usage

```js
var Bundle = require('toolbox-bem-bundle');

var bundle = new Bundle('desktop.bundles/index', { lang: 'ru' });

console.log(bundle.priv.exec); // => Function
console.log(bundle.bemhtml.apply); // => Function
console.log(bundle.name); // => 'index'

var priv = bundle.priv.exec('b-page', data, bundle.name);
var html = bundle.bemhtml.apply(priv);
```

## API

### Bundle(bundlePath, [options])

Создает объект со свойствами:

 * `priv` - Объект с методом `exec`, экспортируемый из priv-файла
 * `privPath` - Путь до priv файла
 * `bemhtml` - Объект с методом `apply`, экспортируемый из bemhtml-файла
 * `bemhtmlPath` - Путь до bemhtml файла
 * `name` - Строка содержащая `path.dirname(bundlePath)`

##### bundlePath  
Type: `String`  

Путь до директории с priv и bemhtml файлами.

##### options
Type: `Object`  

Объект с опциями для Bundle:

###### lang
Type: `String`  

Загружаемый язык. Используется в `join` для получения priv-файла (например `index.priv.ru.js`).

Если язык не определен, то результирующий файл будет называться `index.priv.js`.

###### dev
Type: `Boolean`  
Default: `false`  

Сбрасывать ли кеш require при загрузке priv и шаблонных файлов.

###### cwd
Type: `String`  
Default: `process.cwd()`  

Корневая директория, от которой отсчитывается `bundlePath`.

###### templateExt
Type: `String`  
Default: `bemhtml.js`

Расширение файла с шаблонами (`index.{templateExt}`).

## Benchmarks

```
npm i

node benchmark
```

 op/s       | Comment
------------|---------------------------------------------------------
9,013       | Первая версия
26,335      | Убрали `bind` и оптимизировали вызовы `fs.existsSync`
27,878      | Вынесли загрузку priv и bemhtml в scope
28,362      | Возвращаем целые объекты priv и bemhtml без `bind` их функций

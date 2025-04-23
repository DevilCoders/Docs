# Модульная система API

В первом приближении модули похожи на обычные [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) (require.js) без относительных путей.

Система тесно интегрирована с API и формировалась под его нужды.

Изначально представляла из себя [`ym`](http://npmjs.com/package/ym) с накрученным сверху функционалом описаным ниже.

## Если хочется использовать эти модули для другого проекта

1. Возьми стандартное решение (`require.js`/`webpack`/`SystemJS`/...)
2. "Но очень надо!"
3. Стукни себя по рукам и см. пункт 1

## Создание модульной системы

```js
ym.modules = new ModuleSystem({
    // Параметр для функций с зависимостями.
    dependenciesContext: ym,
    // Название первого бандла.
    initialBudleName: 'panorama',

    // Загрузка бандла с модулями.
    fetchBundle: function (name) {
        return vow.resolve({
            missingModules: [
                'Map',
                /* ... */
            ],
            modules: [
                function(ym) {ym.modules.define('panorama.Panorama' /* ... */)}
            ]
        });
    },
    // Подмена ym для загруженных модулей.
    // Один на все модули.
    createSandbox: function (moduleSystemInstance) {
        return Object.assign({}, ym, { /* extras */ });
    }
})
```

## Базовые возможности

### Объявление модулей

Функция-объявление выполняется при первом запросе модуля, но не при объявлении.

```js
ym.modules.define('namespace.namespace.module', [
    'dependency',
    'anotherDependency'
], function (provide, dependency, anotherDependency) {
    // Вместо возвращения экспортов, как в AMD, в ym надо вызвать функцию.
    provide({});

    // Модуль может отдать экспорты не сразу, а асинхронно с помощью
    // Promise (обычно не нативного, а vow).
    // Используется редко.
    var dataPromise = fetch('//...')
        .then(function (r) { return r.json(); });
    provide.async(dataPromise);

    // DEPRECATED Оставлен для обратной совместимости.
    // Старый способ асинхронного provide'а.
    // Ругается ворнингом в консоль.
    setTimeout(function () {
        provide();
    }, 100);
});

// Зависимости опциональны.
ym.modules.define('namespace.namespace.module', function (provide) {
    // ...
});

// Зависимости могут быть описаны с помощью функции, которая принимает
// config.dependenciesContext и возвращает список модулей.
ym.modules.define('namespace.namespace.module', function (ym) {
    return [
        'dependency',
        ym.env.browser.isIE ? 'implementation.ie' : 'implementation.standards'
    ];
}, function (provide, dependency, implementation) {
    // ...
});
```

### Получение модулей

```js
// Список модулей приводится к массиву.
ym.modules.require('foo.bar').then(function (modules) { modules[0].qux(); });
ym.modules.require(['foo.bar']).then(function (modules) { modules[0].qux(); });

// Удобно использовать vow.spread:
ym.modules.require(['foo', 'bar']).spread(function (foo, bar) {
    console.log(foo.qux() + bar.baz());
});
```

### Динамическая подгрузка модулей

Модульная система при страте грузит бандл указаный в `initialBudleName`. В бандле находятся функции для объявления модулей и имена всех непопавших в бандл модулей.

При попытке получить отсутствующий модуль модульная система запрашивает `full` бандл со всеми доступными модулями в этой версии апи.

## Расширенные возможности

### Альтернативная сигнатура `define` и `require`

```js
ym.modules.define({
    name: 'namespace.module',
    depends: [ /* ... */ ], // function (ym) { return [ ... ]; },
    declarations: function (provide, /* ... */) {
        // ...
        provide(stuff);
    }
});

ym.modules.require({ modules: 'foo' }).spread(function (foo) { /* ... */ });
ym.modules.require({ modules: ['foo'] }).spread(function (foo) { /* ... */ });
```

### Синхронное получение модулей

Можно запросить модуль синхронно, если он уже был загружен и выполнен.

```js
var fooBar = ym.modules.requireSync('foo.bar');
if (!fooBar) {
    // Модуля нет или он еще не загружен, или он объявлен, но не выполнен.
    // Придется загружать асинхронно.
    ym.modules.require('foo.bar').spread(function (fooBar) { /* ... */ });
}
```

### Синхронное объявление модулей

У таких модулей нет функции-объявления и зависимостей:

```js
ym.modules.defineSync({
    name: 'namespace.module',
    module: {
        foo: 'у этого модуля нет функции-объявления, сразу экспорты',
        bar: 42
    }
});
```

### Хранилища модулей

Модули можно хранить по паре строк: `storage` и `key`. Например, это используется для макетов `layout` и пресетов `preset`.

```js
ym.modules.define({
    name: 'namespace.module',

    storage: 'layout',
    key: 'my#placemark', // Можно задать несколько ключей: ['my#1', 'my#2'].

    declaration: function (provide) {
        // ...
    }
});
```

Затем по этой же паре модуль можно получить:

```js
ym.modules.require({ key: 'my#placemark', storage: 'layout' })
    .spread(function (myLayout) {
        // ...
    });

var layout = ym.modules.requireSync({ key: 'my#placemark', storage: 'layout' });
// ...
```

Чаще всего это используется вместе с оберткой `util.AsyncStorage`:

```js
// layout.storage
provide(new AsyncStorage('layout'));

// Где-то еще
var layout = layoutStorage.get('my#placemark');
layoutStorage.require('my#placemark').spread(function () { /* ... */ });
```

### Динамические зависимости

**ВНИМАНИЕ**: динамические зависимости устарели с переходом на бандлы. Новый код с их использованием писать не надо.

Способ борьбы с рекурсивной подгрузкой модулей.

Чаще всего можно встретить для подгрузки под-макетов и имплементаций, конфигурируемых через опции.

```js
ym.modules.define({
    name: 'search.public.interface',

    // Имя зависимости => функция для получения зависимости.
    dynamicDepends: {
        searchProvider: function (data) {
            var x = data.searchProvider;

            // Строка - ссылка на реализацию из хранилища.
            if (typeof x === 'string') {
                // Просим модульную систему загрузить модуль.
                return { key: x, storage: 'search' };
            }

            // Явная ссылка на модуль в хранилище.
            if (typeof x.key === 'string' && typeof x.storage === 'string') {
                // Просим модульную систему загрузить модуль.
                // Формат уже правильный.
                return x;
            }

            // Не ссылка на модуль, а сама имплементация.
            // Модульная система протащит это значение как есть.
            return x;

            // Обычно все выше сокращается до тернарника:
            return typeof x !== 'string' ? x : {
                key: x,
                storage: 'search'
            };

            // Можно вернуть имя модуля строкой:
            return 'namespace.module';

            // Можно вернуть null/undefined, зависимость будет проигнорирована.
            return null;
            return undefined;
        }
    },

    declaration: function (provide) {
        function search(data) {
            // Можно получить синхронно, в макетах спасает от мигания.
            provide.dynamicDepends.getValueSync('searchProvider', data);

            // Получаем модуль асинхронно, если что-то пошло не так и он не был
            // загружен при подгрузке динамических зависимостей.
            // Обертка над ym.modules.require.
            return provide.dynamicDepends.getValue('searchProvider', data)
                .then(function (searchProvider) {
                    return searchProvider.exec(data.query);
                });
        }

        provide(search);
    }
});
```

Получение модулей с динамическими зависимостями.

```js
var data = {
    query: 'foobar',
    searchProvider: 'yandex#coolSearch'
};

// Этот require загрузит и выполнит сразу два модуля:
// - search.public.interface
// - yandex#coolSearch из хранилища search
ym.modules.require({ modules: 'search.public.interface', data: data })
    .spread(function (search) {
        // Модули уже загружены.
        search(data);
    });
```

Динамическая зависимость может указывать на модуль с другими динамическими зависимостями, при этом `data` будет общий:

```js
ym.modules.define({
    name: 'foo',
    dynamicDepends: {
        bar: function (data) { console.log('foo:', data); return 'bar'; }
    },
    declaration: function (provide) { provide(); }
});
ym.modules.define({
    name: 'bar',
    dynamicDepends: {
        nop: function (data) { console.log('bar:', data); return null; }
    },
    declaration: function (provide) { provide(); }
});

ym.modules.require({ modules: 'foo', data: 'DATA' })

// foo: DATA
// bar: DATA
```

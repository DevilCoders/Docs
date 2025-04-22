## 10.0.0

* `.qtools.json` config is not required.

## 9.0.1

* Add mask support (skipping region) for specifying hosts in `.qtools.json` config ([#39](https://github.yandex-team.ru/maps/maps-host-configs/pull/39)).

## 9.0.0

### Breaking changes

* `.qtools.json` config is required ([#37](https://github.yandex-team.ru/maps/maps-host-configs/pull/37)).

## 8.0.1

### Bug fixes

* Fix source maps in npm package. Now source code is included in npm package and source maps works
  as expected ([#36](https://github.yandex-team.ru/maps/maps-host-configs/pull/36)).

## 8.0.0

### Breaking changes

* Drop `Node.js < 8` support.
* Now the package is available by the name of `@yandex-int/maps-host-configs`. The package
  `@yandex-int/ymaps-host-configs` will no longer be updated.

### Bug fixes

* More strict checks for `overrides` parameter ([51fd3ab5605b2b7a8f195834a75dfc06397bb4b2](https://github.yandex-team.ru/maps/ymaps-host-configs/commit/51fd3ab5605b2b7a8f195834a75dfc06397bb4b2)).

## 7.0.0

### Breaking changes

* Disable max age of items in cache by default ([#33](https://github.yandex-team.ru/maps/ymaps-host-configs/pull/33)).

## 6.1.1

* Refactoring: reject `loadConfig()` promise with ConfigNotFoundError when config not found ([#31](https://github.yandex-team.ru/maps/ymaps-host-configs/issues/31)).

## 6.1.0

* Export `Hosts` type in public interface.

## 6.0.0

### Breaking changes

* Use named parameters in `ConfigLoader#get` method.

## 5.0.0

### Bug fixes

* Fix possible reading JSON files using relative path in `hostname`. Now path separator `/` is forbidden.

### Breaking changes

* Minimal supported `Node.js` version is `6`.
* New loader options:

```ts
interface LoaderOptions {
    env: string;
    basePath: string;
    maxCacheAge?: number;
}
```

* `ConfigLoader.get()` rejects promise if configuration file for provided environment doesn't exist.
* Casting of provided environment (i.e. `development -> testing`) was removed.
* Configuration from home directory (i.e. `$HOME/.hosts` and `$HOME/.inthosts`) was removed.
* Use LRU cache instead of cache with timers.

See [#28](https://github.yandex-team.ru/maps/ymaps-host-configs/issues/28) for more information.

## 4.1.1

* Fix including TypeScript declaration to npm package.

## 4.1.0

* Add TypeScript declaration ([#23](https://github.yandex-team.ru/maps/ymaps-host-configs/pull/23)).
* Use [os.homedir()](https://nodejs.org/dist/latest-v8.x/docs/api/os.html#os_os_homedir) instead `process.env.HOME` ([#22](https://github.yandex-team.ru/maps/ymaps-host-configs/pull/22)).

## 4.0.0

### Breaking changes

* Update minimal supported Node.js version to 4 ([#21](https://github.yandex-team.ru/maps/ymaps-host-configs/pull/21)).

## 3.1.1
* Fix possible race condition when read config files ([#19](https://github.yandex-team.ru/maps/ymaps-host-configs/pull/19))

## 3.1.0
* Переопределение хостов через параметр `queryParam` в `ConfigLoader#get` работает в `datatesting`.

## 3.0.1
* Обновление зависимости `fast-memory-cache@~2.0.4`

## 3.0.0

### Обратно несовместимые изменения:

  * Изменение сигнатур

    ```js
    createHostConfigsLoader([environment[, options]]) -> createHostConfigLoader([options])
    createIntHostConfigsLoader([environment[, options]]) -> createIntHostConfigLoader([options])
    ```
  * Изменение параметров `options`.
  * Удален метод `ConfigLoader#getDirectoryPath`
  * Удален метод `ConfigLoader#getEnvironmentName`
  * Метод `ConfigLoader#get` стал асинхронным и возвращает `Promise`.

### Новые возможности:

  * Метод `ConfigLoader#get([hostname[, queryParam]])` принимает второй параметр для
    переопределения хостов.

## 2.1.2
* Обновлена зависимость `object-assign@~4.0.1`
* Версии в dependencies фиксированы через `~`
* Обновлена документация

## 2.1.1
* Fix: object-assign был указан в devDependencies.

## 2.1.0
* Добавлена поддержка пользовательских настроек.

## 2.0.0
* СonfigLoader
  * Добавлена опция disableCache.
  * Опция cacheExpirationTime теперь принимает время в секундах.

## 1.2.0
* createHostConfigsLoader и createIntHostConfigsLoader принимают 2-ым параметром опции аналогичные ConfigLoader.

## 1.1.0
* Добавлен параметр options в ConfigLoader и опция cacheExpirationTime.

## 1.0.0
* Initial release.

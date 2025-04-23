# Changelog

## 2.1.0

### New features

* Return ability of generating `xscript` tokens ([#6](https://github.yandex-team.ru/maps/csrf/pull/6)).

## 2.0.0

### Breaking changes

* Now the package is available by the name of `@yandex-int/csrf`. The package `yandex-csrf` will no longer be updated.
* The `Csrf` class is exported as named entitiy.
* Use UNIX timestamp instead `Date.now()` for generating token (as recommended in [documentation](https://wiki.yandex-team.ru/security/For/web-developers/csrf/#kakgenerirovatiproverjattoken))
* As a consequence, `lifetime` option takes duration is **seconds**.
* Throw `TypeError` if `options.key` is missing in `Csrf` constructor.
* Update minimal version to `Node.js 6`.
* Remove ability of generating `XScript` tokens.

### New features

* Add `TypeScript` support.

## 1.1.0
* Метод `Csrf::isTokenValid()` возвращает `false`, если `token` или `yandexuid` имеют неправильный
  тип ([#2](https://github.yandex-team.ru/maps/yandex-csrf/pull/2)).

## 1.0.0
* Первая версия.

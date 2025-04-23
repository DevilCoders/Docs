# Changelog

## 1.1.0
* Add function-name-signature-conditin rule
* Add no-code-after-export rule
* Add no-code-before-import rule
* Fix npm test script

## 1.0.1
* fix peerDependencies: "eslint": "6.3.0" -> "eslint": "^6.3.0"

## 1.0.0.

### Added
* `asterisk-import` custom rule with tests.
* Required configs and plugins are now included as dependencies. You don't need to install them separately anymore.
* TypeScript for rules and configs. TypeScript support for ESLint.
* Infrastructure for testing rules during development.
* `.npmignore`
* Husky `pre-commit` hook.

### Updated
```
eslint                 4.3.0  ->  6.3.0
eslint-config-loris    8.0.0  ->  9.1.0
eslint-plugin-mocha    4.11.0 ->  6.2.1
eslint-plugin-node     5.1.1  ->  10.0.0
eslint-plugin-unicorn  2.1.2  ->  12.1.0
husky                  0.13.3 ->  3.1.0
```
### Removed
* Everything related to Prop Types.
* `start`, `unit-test` and `precommit` npm scripts.
* `array.prototype.find`
* `babel-eslint`
* `doctrine`
* `eslint-plugin-jsdoc`
* `has`
* `istanbul`
* `mocha`
* `object.assign`

## 0.0.6

* Update package.json for peerDependencies

## 0.0.5

* Shrinkwrap

## 0.0.4

* Up `eslint-plugin-jsdoc`

## 0.0.3

* Up `eslint-config-loris-react`
* Remove `yarn.lock`
* Add `npm-shrinkwrap.json`

## 0.0.2

* Обновил правила, добавил разные конфигурации
* MAPSINFRA-97: Перевести CI с drone в teamcity

## 0.0.1

* MAPSINFRA-51: Вынести исправленные правила eslint в отдельный пакет

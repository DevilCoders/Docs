Wmfront Codestyle
=================

## Установка

```bash
npm install --save-dev git://github.yandex-team.ru/wmfront-common/codestyle.git
```

## JSHint

Положите в папку проекта файл `.jshintrc`, в котором определите опцию `extends` и переопределите нужные параметры:

```json
{
  "extends": "node_modules/wmfront-codestyle/jshint/jshintrc",
  "globals": {
    "BEM": true
  }
}
```

## JSCS

Положите в папку проекта файл `.jscs.json`, задайте плагин и пресет, переопределите необходимые опции:

```json
{
  "plugins": [ "wmfront-codestyle/jscs" ],
  "preset": "wmfront",
  "excludeFiles": [
    ".npm"
  ]
}
```

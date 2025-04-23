# Геоадмины: фронтенд

## Как установить
```bash
$ cd proto
$ npm install
$ bower install
$ grunt
```

Для сборки продакшен версии выполнить `grunt dist`.

## Структура директорий

```
.bem - конфиг для enb
.ldm
app - код приложения
app/common - абстрактные классы
app/controls - контролы карты
app/modules - подключаемые модули
app/index.js - точка входа с основным конфигом
common.blocks
desktop.blocks - кастомные BEM блоки
desktop.bundles - шаблоны
vendors - туда ставяться зависимости из bower
```

## Локализация

Переводы строк из шаблонов хранятся в блоке gettext.

Переводить админку на все языки странно, поэтому переводы не отправляются в танкер,
их нужно поддерживать самостоятельно.

Для удобства сделан маленький велосипед `grunt i18n`.
Он анализирует шаблоны и вытаскивает оттуда ключи.
А так же сообщает о устаревших переводах и новых ключах.

## Зависимости о которых нужно знать

- [LMD](http://lmdjs.org)
- [Backbone](http://backbonejs.org)
- [Backbone.Marionette](http://marionettejs.com)
- [Backbone.YMaps](https://github.com/smacker/backbone-ymaps)
- [Backbone.Relational](https://backbonerelational.org)
- Lego [Islands](http://beta-lego.yandex-team.ru/)

## Что еще нужно знать

- Над всеми Marionette View написаны сделаны обертки с BEM Mixin, позволяющие декларативно вешать события на бем-блоки
- Шаблоны при рендере обрабатываются underscore шаблонизатором с mustache-like синтаксисом
- Перед сборкой код проверяется при помощи JSLint&JSCS
- Ошибки с сервера обрабатываются при помощи переобределения Backbone.ajax (utils/ajax.js)

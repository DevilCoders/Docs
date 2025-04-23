## Мульти-плагин
Плагин для webpack. Используется для мультипликации бандлов.

### Задача
На момент написания СЕРП поддерживает 9 локалей см файл `.i18n.conf.js`

Стандартный способ собрать несколько бандлов для разных языков это запуск webpack в режиме [мультикомпиляции](https://webpack.js.org/configuration/configuration-types/#exporting-multiple-configurations)

Основная проблема такого подхода – время сборки увеличивается в те самые 9 раз.

Этот плагин – решение данной проблемы.

### Схема работы
Плагин заточен на текущее ядро интернализации и делает два действия:

* Мультиплицирует один чанк на 9 (по количеству переданных локалей)
* Подменяет контент файлов отвечающих за локализацию

#### Мультипликация
Мы клонируем основной чанк 9 раз, и добавляем в склонированные чанки все js модули.
При этом за css отвечает основной чанк.

было:
```
bundle.js
bundle.css
```

стало:
```
bundle.js
bundle.css
bundle.en.js
bundle.tr.js
bundle.tt.js
...
bundle.kk.js
```

bundle.js - считается дефолтным и содержит локаль `ru`.

bundle.css - считается общим. css один на все локали.

#### Подмена контента
Подмена происходит в двух местах:

* установка языка
* загрузка ключей


##### Установка языка

Используется опции:

```js
 simpleReplaceMatcher: /config\/i18n.js/,
 multi: [{
   simpleReplace: ['I18N_LANG', 'ru']
 }, {
   simpleReplace: ['I18N_LANG', 'en']
 },
...
 ]
```

В каждом бандле есть файл config.i18n.js
В которм есть строка:
```js
setI18nLang(I18N_LANG);
```
которая будет подменена на
```js
setI18nLang('ru');
```
или
```js
setI18nLang('en');
```

В зависимости от локали.

##### Загрузка ключей

Используется опции:

```js
replaceSourceMatcher: /\.i18n\/index.ts/,
disconnectMatcher: /\.i18n\/((?!index).)*.ts/,
 multi: [{
   replaceModule: [ `export * from './ru';`, 'ru', './ru' ],
   disconnectModulesExcept: 'ru.ts',
 }, {
   replaceModule: [ `export * from './en';`, 'en', './en' ],
   disconnectModulesExcept: 'en.ts',
 },
...
 ]
```

Когда плагин встречает файлы `feature.i18n/index.ts` c контентом:
```js
export * from './be';
export * from './en';
export * from './id';
export * from './kk';
export * from './ru';
export * from './tr';
export * from './tt';
export * from './uk';
export * from './uz';
```

Он подменяет их на:
```js
export * from './ru';
```

```js
export * from './en';
```

В зависимости от локали.
При этом из графа сборки конкретного бандла удаляются все ненужные зависимости.


### Проблемные места
* Плагин получился сильно низкоуровневый – Используются внутренние механизмы webpack для построения модулей
* Плагин сильно заточен на текущее ядро i18n и текущую сборку реакт бандлов.

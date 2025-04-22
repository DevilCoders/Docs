# React i18n

Локализаций React-компонент реализована по тому же принципу что и в `islands`, но есть *нюансы*.

На данном этапе мы рассчитываем что пользователи `lego-on-react` используют `webpack` для сборки.

Примеры конфигураций `webpack` сборки можно посмотреть в [репозитории](https://github.yandex-team.ru/yeti-or/lego-react-example)

## Lego-as-dist

Для правильной работы ключей в формате танкера необходим специальный лоадер кейсетов. Установить его можно командой:

```bash
npm i -D webpack-bem-i18n-loader
```

В `webpack.config.js` добавляем лоадер:

```js
    module: {
        loaders: [{
            test: /\.i18n\//,
            loader: 'webpack-bem-i18n-loader'
        }]
    },
```

Для того чтобы определить локаль для бандла необходимо пробросить её через `DefinePlugin`:

```js
    plugins: [new webpack.DefinePlugin({
        'process.env': {
            BEM_LANG: JSON.stringify(process.env.BEM_LANG || 'ru')
            // или, что тоже самое
            // REACT_APP_BEM_LANG: JSON.stringify(process.env.REACT_APP_BEM_LANG || 'ru')
        }
    })],
```

## Lego-as-src

Если вы используете `islands` как уровень переопределения, то вы уже знакомы с `webpack-bem-loader`.

Для корректной работы вам нужно изменить опции на следующие:

```js
  bemLoader: {
    naming: 'origin', // пресет найминга см https://github.com/bem-sdk/bem-fs-scheme/blob/master/lib/presets/origin.js
    techs: ['js', 'css'], // набор технологий по которым раскравается bem-import
    techMap: {
        js : ['react.js'] // матчинг технологий на расширения файловой системы
    },
    langs: ['ru', 'en'], // набор возможных языков
    levels: [paths.legoCommonBlocks, paths.legoDesktopBlocks,  paths.appBlocks], // уровни переопределения
  },

```

Для правильной работы ключей в формате танкера необходим специальный лоадер кейсетов. Установить его можно командой:

```bash
npm i -D webpack-bem-i18n-loader
```

В `webpack.config.js` добавляем лоадер:

```js
    module: {
        loaders: [{
            test: /\.i18n\//,
            loader: 'webpack-bem-i18n-loader'
        }]
    },
```

Для того чтобы определить локаль для бандла необходимо пробросить её через `DefinePlugin`:

```js
    plugins: [new webpack.DefinePlugin({
        'process.env': {
            BEM_LANG: JSON.stringify(process.env.BEM_LANG || 'ru')
            // или, что тоже самое
            // REACT_APP_BEM_LANG: JSON.stringify(process.env.REACT_APP_BEM_LANG || 'ru')
        }
    })],
```

После этого вы можете создавать свои кейсеты и вызывать их.

Пользовательский уровень:

```js
blocks/
  my-block/
    my-block.js
    my-block.css
    my-block.i18n/
      en.js
      ru.js
```

И в файле `my-block.js`:

```js
import i18n from 'b:my-block t:i18n';
import attachI18N from 'b:attach t:i18n'; // Лего

console.log(i18n('key')) // 'value'
console.log(attachI18N('button-text')) // 'Select file'
```

В зависимости от переданной переменной окружения `BEM_LANG`,
функция `i18n` будет возвращать значения из нужного кейсета.

## Остались вопросы?

Пишите нам в Slack [lego-team.slack.com](https://lego-team.slack.com) канал [#support](https://lego-team.slack.com/messages/support/)
или на рассылку [lego@yandex-team.ru](mailto:lego@yandex-team.ru?subject=Вопрос по React)

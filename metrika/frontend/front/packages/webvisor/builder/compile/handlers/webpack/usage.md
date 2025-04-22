# Обработчик JS-бандлов

Данный обработчик использует Webpack 3 для реализации функционала.

# Пример

```javascript
exports.webpack   = {
  entry: 'dev/client/javascripts/playlist/index.js',
  output: {
    filename        : 'list.js',
    libraryTarget   : 'var',
    library         : 'test'
  }
}
```

# Параметры настройки обработчика

Весь объект `webpack` представляет из себя стандартный набор настроек Webpack 3, которые можно найти в [документации](https://webpack.js.org/configuration/).

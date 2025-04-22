# Плагин для шифрования чанков с помощью антиадблочной прокси

## Установка

Установка через npm:
```shell
$ npm install --save-dev @yandex-int/antiadblock-webpack-plugin
```

## Использование

Плагин добавляется стандартным образом:

```javascript
const AntiadblockWebpackPlugin = require('@yandex-int/antiadblock-webpack-plugin');

plugins: [
  new AntiadblockWebpackPlugin()
]
```

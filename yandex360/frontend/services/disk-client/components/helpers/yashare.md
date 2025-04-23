# YaShare

Хелпер, которы помогает работать с js-апи [стандартных яндексовых поделяшек](https://tech.yandex.ru/share/).
Умеет загружать библиотеку и создавать новый экземпляр поделяшек.

## API

```javascript
var helperYaShare = require('helpers/yashare.js');

helperYaShare.init({
    // @see https://tech.yandex.ru/share/doc/dg/concepts/share-button-ov-docpage/
    element: 'ya-share',
    elementStyle:  {
        type: 'none'
    }
    ...
})
    .then(function(yashare) {
        // yashare — экземпляр блока поделяшек
    })
```
### init

Асинхронно загружает библиотеку `//yastatic.net/share/share.js` и создает новый экземпляр поделяшек. Принимает [все доступные параметры](https://tech.yandex.ru/share/doc/dg/concepts/share-button-ov-docpage/).

Возвращает промис, который резолвится экземпляром блока.

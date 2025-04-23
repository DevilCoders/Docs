# Стабы для картинок

## Использование на сервере
```js
const { proxy } = require('proxy-stub-utils');

proxy.wrap('https://example.com/image.png');
// https://mmui-png-stub.yandex-team.ru/?url=https%3A%2F%2Fexample.com%2Fimage.png

proxy.wrap('https://example.com/image.png', {
    strategy: 'pngPatternStub'
});
// https://mmui-png-stub.yandex-team.ru/?strategy=pngPatternStub&url=https%3A%2F%2Fexample.com%2Fimage.png

proxy.wrap({
    w: 800,
    h: 600,
    border: 30
});
// https://mmui-png-stub.yandex-team.ru/?border=30&h=600&w=800

proxy.unwrap('https://mmui-png-stub.yandex-team.ru/?url=https%3A%2F%2Fexample.com%2Fimage.png');
// { url: https://example.com/image.png }
```

## Использование на клиенте

Для автотестов [в клиентский JS](sakhalin/blocks-common/b-page/__js/b-page__js.priv.js) добавляется хелпер `window.Ya.MM.proxy.wrap`.
Для video-tv это происходит [тут](video/blocks-tv/b-page/b-page.common.js).

```js
window.Ya.MM.proxy.wrap('https://ya.ru/img.png', { border: 10 });
// https://mmui-png-stub.yandex-team.ru/?border=30&url=https%3A%2F%2Fya.ru%2Fimg.png
```

## Дополнительно:
* В .templar/plugins/cache-key.js при формировании ключа кэша из параметра url убираются знания про прокси картинок, чтобы хост/путь прокси не влиял на использование кэшей на проекте.
* В Видео оборачивание в прокси: [на клиенте](video/blocks-common/thumb-url/_client/thumb-url_client_interface.js) и [на сервере](video/blocks-common/thumb-url/_server/thumb-url_server_interface.common.js)

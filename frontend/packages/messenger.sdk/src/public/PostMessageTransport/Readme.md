# PostMessageTransport

Транспорт сообщений через PostMessage. Использует iframe.

## Использование

```javascript
const { PostMessageTransport } = require('@yandex-int/messenger.sdk/public');

const transport = new PostMessageTransport({
    iframeUrl: '',
    scopeParams: {
        // Ключ - название скоупа
        // Значение - параметры для скоупа
    }
})
```

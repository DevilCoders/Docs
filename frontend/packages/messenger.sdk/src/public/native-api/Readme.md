# NativeTransport

Клиент для использования нативных методов месссенджера в Ябро.

На данный момент пакет не поддерживает работу с заблокированными куками. Т.е. работает только для [*.]yandex.{tld}

## Использование

```javascript
const { PostMessageTransport, createNativeTransport, NATIVE_TRANSPORT_SCOPE } = require('@yandex-int/messenger.sdk/public');

const postMessageTransport = new PostMessageTransport({
    iframeUrl: 'https://yandex.ru/chat/iframe-api',
    scopeParams: {
        [NATIVE_TRANSPORT_SCOPE]: {}
    }
});
const api = createNativeTransport(postMessageTransport);

// Доступно ли нативное апи
const isApiAvailable = await api.apiCheck();

//...

// Открыть чат в балуне Ябро
await api.showChat(...params);
```

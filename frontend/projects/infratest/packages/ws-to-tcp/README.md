# ws-to-tcp

Инструмент позволяет перенаправлять трафик удаленного сервера, который отдаётся по *WebSocket*, на локальный *TCP*-порт.

## Установка

```bash
$ npm install @yandex-int/ws-to-tcp --registry=http://npm.yandex-team.ru
```

## Использование

### API

```javascript
const { WebSocketToTcpProxy } = require("@yandex-int/ws-to-tcp");

const webSocketUrl = 'wss://';
const tcpPort = 5901;

const proxy = new WebSocketToTcpProxy(webSocketUrl, tcpPort, {
    env: { NODE_TLS_REJECT_UNAUTHORIZED: '0' }, // доопределение окружения TCP-сервера
});
// const proxy = new WebSocketToTcpProxy(webSocketUrl); // TCP-сервер поднимется на свободном порту

proxy.open()
    .then((tcpPort) => tcpPort)
    .then(() => proxy.close());
```

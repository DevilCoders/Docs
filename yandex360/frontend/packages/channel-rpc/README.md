[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/packages/channel-rpc&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/channel-rpc)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/packages/channel-rpc&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/channel-rpc)

## Channel RPC

Простейший RPC над всем у чего есть postMessage.

### Использование
```js
import RPC from '@ps-int/channel-rpc';

// Передаем scope, в котором будут обрабатываться запросы.
// Передаем функцию, которая будет вычислять получателя.
const rpc = new RPC('/', () => window);

// Подписаться на событие пришедшее по каналу.
rpc.on('someEvent', () => {});

// Создать реакцию на запрос пришедший по каналу.
// Реакция может вернуть асинхронный результат в канал.
rpc.registerCommand('someCommand', async () => {
    const result = await someMethod();
    return result;
});

// Отправить в канал запрос на выполнение события.
rpc.sendEvent('someEvent', params);

// Отправить в канал запрос на выполнение команды и дождаться результата.
const response = await rpc.sendRequest('someCommand', params);

// Подключить обработчик с куществующему интерфейсу с message API
window.addEventListener('message', ({ data, ports }) => rpc.handle({ data, ports }));
```

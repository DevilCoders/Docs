# @yandex-int/si.ci.telegraph

Высокоуровневый клиент для работы с Telegraph API.

В отличие от [`@yandex-int/si.ci.telegraph-client`](../telegraph-client) предоставляет композитные функции, комбинирующие поведение низкоуровневых вызовов.

## Установка

```bash
npm install @yandex-int/si.ci.telegraph --registry=https://npm.yandex-team.ru
```

## Использование

Пример использования:

```js
const client = require('@yandex-int/si.ci.telegraph');

const token = '...';
// Опциональный параметр, есть значение по умолчанию.
const baseUrl = 'https://telegraph.yandex-team.ru/api/v3/';

const telegraph = client.factory({ token, baseUrl });

// Найти среди всех доступных очередь по её имени.
await telegraph.findQueueByName('76800-2')

// Удалить всех участников из очереди по её ID.
await telegraph.clearQueueById('27');

// Удалить всех участников из очереди по её имени.
await telegraph.clearQueueByName('76800-1');

// Добавить указанные номера в очередь по её имени.
await telegraph.addMembersToQueue('76800-2', ['6733', '2215']);

// Очистить очередь по её имени, затем добавить переданные номера.
await telegraph.replaceQueueMembersByName('76800-2', ['6733', '2215']);
```

## Отладка

Включить вывод отладочной информации можно с помощью переменной окружения:

```bash
export DEBUG=si:ci:telegraph
```

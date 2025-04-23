# @yandex-int/si.ci.telegraph-client

Низкоуровневый клиент для работы с Telegraph API (приложение Asterisk).
Нет никакой интеграции со Staff, работать можно только с телефонными номерами.

Более высокоуровневую реализацию см. в [`@yandex-int/si.ci.telegraph`](../telegraph).

**Telegraph** — внутренняя разработка Яндекса, обёртка над VoIP приложениями вроде [Asterisk] или [CUCM] (_Cisco Unified Communications Manager_).

Предоставляет разработчикам Яндекса агрегированный доступ к различным частям телефонии.
Некоторые части API знают о другой инфраструктуре Яндекса (Staff, GAP), но прямой интеграции нет.
Например, невозможно добавить в очередь звонков телефон человека по его логину.

* [Краткое описание схемы][telefonia].
* [Описание API][api-docs].

## Установка

```bash
npm install @yandex-int/si.ci.telegraph-client --registry=https://npm.yandex-team.ru
```

## Использование

Пример использования:

```js
const client = require('@yandex-int/si.ci.telegraph-client');

const token = '...';
// Опциональный параметр, есть значение по умолчанию.
const baseUrl = 'https://telegraph.yandex-team.ru/api/v3/';

const telegraphClient = client.factory({ token, baseUrl });

// Получить список доступных авторизованному пользователю очередей с настройками.
await telegraphClient.listAvailableQueues();

// Получить настройки и список участников очереди по её ID.
await telegraphClient.fetchQueueById('27');

// Найти по номеру телефона человека среди привязанных к доступным очередям.
await telegraphClient.fetchMemberByExten('6990');

// Привязать номер телефона в очередь по её имени (не ID).
await telegraphClient.addMemberToQueue('76800-1', '6990');
// Префикс 55 означает "определить мобильный по внутреннему номеру и позвонить".
await telegraphClient.addMemberToQueue('76800-2', '556990');

// Удалить привязанный номер по уникальному идентификатору привязки.
await telegraphClient.deleteMemberByUniqueId('662439');
```

`token` — доменный токен со скоупом **Телеграф API**.

![Telegraph scope](./assets/telegraph-scope.png)

Получить его можно, пройдя по ссылке _"Получение токена для авторизованного пользователя"_ из заголовка [документации по API][api-docs].
Однако, этим дело не ограничится и нужно попросить [help@](mailto:help@yandex-team.ru) соответствующему пользователю дать права на:

* чтение и запись в очереди в Asterisk, которыми вы владеете;
* добавление/удаление в очередь необходимых сотрудников или групп.

## Отладка

Включить вывод отладочной информации можно с помощью переменной окружения:

```bash
export DEBUG=si:ci:telegraph-client
```

[Asterisk]: https://www.asterisk.org/
[CUCM]: https://www.cisco.com/c/en/us/products/unified-communications/unified-communications-manager-callmanager/index.html
[telefonia]: https://wiki.yandex-team.ru/VladimirPiskun/Telefonija-na-telegrafe/
[api-docs]: https://telegraph.yandex-team.ru/api/v3/

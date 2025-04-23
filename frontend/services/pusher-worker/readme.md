Воркер живет под фейковым scope: `/notifications/`.

В реальности такого пути (`https://yandex.<tld>/notifications/`) не существует, но воркер можно повесить на него. 
Это позволяет обрабатывать пуши, не замедяя запросы, которые не имеют
к уведомлениям никакого отношения.

## Структура модулей

```
src
├── messenger // модуль обрабатывающий входящие сообщения в воркер
│   └── ...
│
├── notifications // вся работа с хранилищем indexedDB в воркере осуществляется через этот модуль
│   └── YaIDBRequest // promisify над IDBRequest
│   └── YaIDBTransaction // promisify над IDBTransaction
│
├── pusher // модуль отвечающий за отображение пушей
│   └── Task // планирует выполнение задачи
│   └── TaskManager // обслуживает задачи
│   └── Statistics // отвечает за статистику
│   └── ...
│
├── Sup // модуль осуществляющий подписку, реализующий API СУПа
│   └── ...
│
├── YaServiceWorker // общий модуль для взаимодействия с ServiceWorker
│
└── // в корне лежат только точки входа в приложение
    └── pusher-worker // только обработка отображения пушей
    └── sup-worker // pusher-worker + логика про подписку в СУПе
```

## Тестирование

Есть два вида тестов:
* `*.unit.ts`
    
    Тесты выполняются в контексте Node.JS, 
    запускаются командой `npm run unit:default`,
    прогоняются автоматически в PR и при влитии на этапе Merge Queue.
    
* `*.test.ts`

    Тесты выполняются в контексте браузера,
    запускаются командой `npm run unit:karma`,
    **прогоняются вручную перед созданием PR**.

В тестах есть модули: `sinon`, `chai` (рекомендуется использовать только `assert` из него).

## Используемые хранилища

* **indexedDB**
    
    Для служебных нужд воркер использует indexedDB хранилище с именем `notifications`.
    Больше информации о структуре и выпущенных версиях можно узнать в
    [changelog.md](src/notifications/changelog.md)
    
## Доступ

* **Production**

    Файлы воркера можно получить по следующей схеме:
    `https://yandex.<tld>/service-workers/pusher-worker/<platform>/<name>.js`
    
    `<platform>` - одно из следующих значений: `desktop`, `pad`, `phone`.
    
    `<name>` - одно из следующих значений: `pusher`, `sup`.
    
    Примеры: 
    * https://yandex.ru/service-workers/pusher-worker/desktop/sup.js
    * https://yandex.ru/service-workers/pusher-worker/pad/sup.js
    * https://yandex.ru/service-workers/pusher-worker/phone/sup.js

* **Testing**

    Файлы воркера можно получить по следующей схеме:
    `http://service-workers.yandex.net/<bucket>/pusher-worker/<hash>/<platform>/<name>.js`

    `<bucket>` - одно из следующих значений: 
    * `service-workers` имя бакета для продакшен воркер-файлов.
    * `service-workers-test` имя бакета для тестовых версий воркер-файлов.
    
    `<hash>` - только для бакета `service-workers-test`, принимает одно из следующих значений:
    * `номер-PR/хэш-последнего-коммита`
    * `версия-пакета`
    
    `<platform>` - одно из следующих значений: `desktop`, `pad`, `phone`.
        
    `<name>` - одно из следующих значений: `pusher`, `sup`.
    
    Примеры:
    * http://service-workers.yandex.net/service-workers/pusher-worker/desktop/sup.js
    * http://service-workers.yandex.net/service-workers-test/pusher-worker/v1.1.1/desktop/sup.js
    
    Из примеров выше видно, чтобы работать через тестовые ручки, необходимо **настроить прокси на домен** 
    `http://service-workers.yandex.net/`.
    
    Примеры:
    * https://hamster.yandex.ru/service-workers/pusher-worker/desktop/sup.js
    * https://hamster.yandex.ru/service-workers-test/pusher-worker/v1.1.1/desktop/sup.js

## См. также

* [pusher](https://github.yandex-team.ru/IMS/vh-selfservice/tree/develop/packages/vh-pusher)
* [pusher-middleware](https://github.yandex-team.ru/IMS/vh-selfservice/tree/develop/packages/vh-pusher-middleware)

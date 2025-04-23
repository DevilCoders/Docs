# Плагин для полинга кол-ва непрочитанных сообщений

Позвозляет получить кол-во непрочитанных сообщений без открытия мессенджера.
При этом после открытия виджета - полинг прекращается и начинают использоваться данные мессенджера.

В случае если сервис находится не на домене `yandex.{tld}` или `*.yandex.{tld}`
необходимо обратиться к дежурному мессенджера.

Для упращенной инициализации плагина можно использовать две фабрики:

`yandexUnreadCounterFactory` - для внешних сервисов яндекса

`yandexTeamUnreadCounterFactory` - для внутренних сервисов яндекса

## Пример

```ts
import {
    Widget,
    Config,
    yandexUnreadCounterFactory,
} from '@yandex-int/messenger.widget';

const widget = new Widget(new Config().create());
const unreadCounter = yandexUnreadCounterFactory();

unreadCounter.onChanged
    .addListener((value: UnreadCounterData) => console.log(value))

widget
    .addPlugin(unreadCounter)
    .init();
```

Доступны два клиента полинга из пакета `@yandex-int/messenger.unread-counter`

`UnreadCounter` - для получения данных используется полинг https ручки мессенджера
Подходит для интеграции в сервисы яндекса. Необходимо разрешить `CORS` на yandex.{tld}

`UnreadCounterIframeClient` - для получения данных используется iframe
(подходит при интеграции во внешние сервисы)

## Пример с `UnreadCounter`

```ts
import { UnreadCounter } from '@yandex-int/messenger.unread-counter';
import {
    Widget,
    Config,
    UnreadCounterPlugin,
    YANDEX_UNREAD_COUNTER_ENDPOINT,
} from '@yandex-int/messenger.widget';

const widget = new Widget(new Config().create());
const unreadCounter = new UnreadCounterPlugin(
    YANDEX_UNREAD_COUNTER_ENDPOINT,
    (params) => new UnreadCounter(params)
);

unreadCounter.onChanged
    .addListener((value: UnreadCounterData) => console.log(value))

widget
    .addPlugin(unreadCounter)
    .init();
```

# Конструктор

**constructor**(unreadUrl: string, unreadCounterFactory?: (params: [UnreadCounterParams](./interfaces.md#unreadcounterparams)): [UnreadCounterClient](./interfaces.md#unreadcounterclient)): [UnreadCounterPlugin](./interfaces.md#unreadcounterplugin)

`unreadUrl`: string

URL ручки непрочитанных сообщений

`unreadCounterFactory`: (params: [UnreadCounterParams](./interfaces.md#unreadcounterparams)): [UnreadCounterClient](./interfaces.md#unreadcounterclient)

Фабрика клиента получения кол-ва непрочитанных из внешнего источника
Стандартные клиенты лежат в пакете `@yandex-int/messenger.unread-counter`

---

`onChanged`: *[Event](./interfaces.md#event)\<[UnreadCounterData](./interfaces.md#unreadcounterdata)>*

>

Вызывется при изменении значения непрочитанных сообщений

---

## Фабрика плагина непрочитанных сообщений для сервисов яндекса

Если сервис находится не на домене yandex.{tld}/*.yandex.{tld},
необходимо обратиться дежурному мессенджера для добавления домена в разрешенные

**yandexUnreadCounterFactory**(): [UnreadCounterPlugin](./interfaces.md#unreadcounterplugin)

## Фабрика плагина непрочитанных сообщений для внутренних сервисов яндекса

**yandexTeamUnreadCounterFactory**(): [UnreadCounterPlugin](./interfaces.md#unreadcounterplugin)
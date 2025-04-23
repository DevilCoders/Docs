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
import { Widget, Config } from '@yandex-int/messenger.widget';
import {
    yandexUnreadCounterFactory,
} from '@yandex-int/messenger.widget/plugins';

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
import { Widget, Config } from '@yandex-int/messenger.widget';
import {
    UnreadCounterPlugin,
    YANDEX_UNREAD_COUNTER_ENDPOINT,
} from '@yandex-int/messenger.widget/plugins';

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

(unreadUrl: string, unreadCounterFactory?: undefined): [UnreadCounterPlugin](./interfaces#unreadcounterplugin)

`unreadUrl`: string

URL ручки непрочитанных сообщений

`unreadCounterFactory`: undefined

Фабрика клиента получения кол-ва непрочитанных из внешнего источника
Стандартные клиенты лежат в пакете `@@yandex-int/messenger.unread-counter`

`onChanged`: *[Event](./interfaces#event)\<[UnreadCounterData](./interfaces#unreadcounterdata)>*

>

---

Вызывется при изменении значения непрочитанных сообщений
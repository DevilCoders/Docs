## Интероп с мобильным приложением

Для общения между мобильным приложенем и шторкой используется библиотека @ps-int/interop

Главной спецификацией сигналов и транспорта является @ps-int/js-bridge. Из нее можно получить преднастроенный транспорт для @ps-int/interop, а так же базовые сигналы.

```ts
import {
    AppType,
    BaseEvents,
    BaseEventsNames,
    getInteropRecieverTransport,
    getInteropSenderTransport,
} from '@ps-int/js-bridge';

type SendEvents = {}
type ReceiveEvents = {}

const senderTransport = getInteropSenderTransport(window, environmentConfig.appType);
const receiverTransport = getInteropRecieverTransport(window);

const sender = new Sender<BaseEvents & SendEvents>(senderTransport);
const receiver = new Receiver<ReceiveEvents>(receiverTransport);

sender.sendEvent({name: BaseEventsNames.DOMReady});
```

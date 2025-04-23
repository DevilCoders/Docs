# @ps-int/js-bridge

Библиотека, описывающая спецификацию общения веб-вью и мобильного приложения.

Для отправки\приема сигналов нужно использовать @ps-int/interop.

### Транспорт
Для создания транспорта нужно использовать функции getInteropSenderTransport, getInteropRecieverTransport.

```js
import {getInteropSenderTransport, getInteropRecieverTransport} from '@ps-int/js-bridge';

const senderTransport = getInteropSenderTransport(window, AppType.IOS);
const receiverTransport = getInteropReceiverTransport(window);
```
### Базовые события

Список событий c описанием [тут](./src/signals.ts)

```js
import type {BaseEvents} from '@ps-int/js-bridge';
import {BaseEventsNames} from '@ps-int/js-bridge';

const sender = new Sender<BaseEvents>(senderTransport);

sender.send({name: BaseEventsNames.DOMReady});
```

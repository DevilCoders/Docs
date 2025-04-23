## Sender

Сервис для отправки сообщений. Связывает описание событий и транспорт.

В качестве транспорта поддерживает любой объект, реализующий интерфейс ITransportSender

Пример:

```ts
const windowPostMessageTransport = WindowPostMessageTransport('https://mail.yandex.ru');

type Events = {
    'event1': string,
    'event2': never
}

const sender = new Sender<Events>(windowPostMessageTransport);

sender.sendEvent({name: 'event1', payload: '123'});
```

### Параметры для транспорта
Sender поддерживает проксирование параметров транспорта. 

Для правильной работы типизации параметров транспорта Sender явно нужно указать тип транспорта.

```ts
const windowPostMessageTransport = WindowPostMessageTransport('https://mail.yandex.ru');

type Events = {
    'event1': string,
    'event2': never
}

const sender = new Sender<Events, WindowPostMessageTransport>(windowPostMessageTransport);
sender.sendEvent({name: 'event2'}, {transferable: [new Uint8Array([1,2,3])]});


```

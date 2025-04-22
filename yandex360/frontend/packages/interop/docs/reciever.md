## Receiver

Сервис для приема сообщений. Связывает описание событий и транспорт.

В качестве транспорта поддерживает любой объект, реализующий интерфейс ITransportReceiver

Пример:
```ts
const windowPostMessageTransport = new WindowPostMessageTransport('https://mail.yandex.ru');

type Events = {
    'event1': string,
    'event2': never
}

const receiver = new Receiver<Events>(windowPostMessageTransport);

receiver.subscribe('event1', (someString) => {
    console.log(someString);
})
```

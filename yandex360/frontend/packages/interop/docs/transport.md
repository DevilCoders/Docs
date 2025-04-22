## Transport

Для реализации транспорта есть 2 интерфейса:
1. ITransportSender
2. ITransportReceiver

Их соответствующие реализации передаются в Sender и Receiver.
Реализации могут быть как 2 разных класса, так и один.

Примеры:

```ts
// Один класс
class WindowPostMessageTransport implements ITransportSender<{
    transferable?: Transferable[];
    anyTargetOrigin?: boolean
}>, ITransportReceiver {
    public send({name, payload}: {name: string, payload?: unknown}, options?: {}): void {}
    public subscribe(cb: ({name, payload}: {name: string, payload?: unknown}) => void): void {}
}
```

### Базовые реализации транспорта

1. Window.postMessage
2. WKWebViewPostMessage
3. AndroidOnEvent

`

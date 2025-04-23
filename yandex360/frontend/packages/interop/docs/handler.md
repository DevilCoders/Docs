## Executer

Сервис для обработки сообщений и ответа на них.

Связывает Sender и Receiver.

```ts
type Commands = {
    'command1': Command<{ param1: string; param2?: string }, { result1: string; result2?: string }>;
    'command2': Command<{ param3: number; param4: string }, {ololo: number }>;
}

const windowPostMessageTransportSender = new WindowPostMessage('*');
const windowPostMessageTransportReceiver = new WindowPostMessage('https://rideorgtfo-monoliza.tavern-dev.mail.yandex.ru');

const receiver = new Receiver<CommandsToReceiverEvents<Commands>>(windowPostMessageTransportReceiver);
const sender = new Sender<CommandsToSenderEvents<Commands>>(windowPostMessageTransportSender);

const handler = new Handler<Commands, typeof receiver, typeof sender>(sender, receiver);

handler.init({
    command1: payload => {
        payload.param2;

        return {
            result1: '123',
        };
    },
    
    command2: async (payload) => {
        payload.param3;
        
        await Promise.resolve();
        
        return {
            ololo: 123
        }
    }
});
```

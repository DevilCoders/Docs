## Executer

Сервис для отправки сообщений и ожидания ответа от них.

Связывает Sender и Receiver.

Пример:
```ts
import { WindowPostMessageTransport} from "@ps-int/channel-rpc-2/lib/transport";
import { CommandsToReceiverEvents, CommandsToSenderEvents } from "@ps-int/channel-rpc-2/lib/types";

type Commands = {
    'command1': Command<{ param1: string, param2?: string }, { result1: string, result2?: string }>,
    'command2': Command<Record<string, never>, {ololo: number }>
}

const windowPostMessageTransportSender = new WindowPostMessageTransport('*');
const windowPostMessageTransportReceiver = new WindowPostMessageTransport('https://rideorgtfo-monoliza.tavern-dev.mail.yandex.ru');

const receiver = new Receiver<CommandsToReceiverEvents<Commands>>(windowPostMessageTransportReceiver)
const senderForTransferable = new Sender<CommandsToSenderEvents<Commands>, WindowPostMessageTransport>(windowPostMessageTransportSender);
const executer = new Executer<Commands, typeof receiver, typeof senderForTransferable>(senderForTransferable, receiver);

executer.execute('command11', {}, {timeout: 500}).then((data) => {
    data.result1
})
executer.execute('command2', {}, {}, {transferable: [], anyTargetOrigin: true}).then((data) => {
    data.requestId
})
```



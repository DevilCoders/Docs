# @yandex-market/mbo-messages

Библиотека для отображения сообщений

## Установка
```bash
npm install @yandex-market/mbo-messages
```
## Простой пример использования

```typescript

import { createMessagesReducerFactory } from '@yandex-market/mbo-messages';
export const { messageReducer, messageActions, messagesSelector } = createMessagesReducerFactory('globalMessages');

export const rootReducer = combineReducers<RootState>({
  globalMessages: messageReducer,
});

const messageFormatter = (message: Message) => {
  if (message.details?.customDetails) {
    return (
      <div>
        <h3>Custom details</h3>
        <div>{message.details.mboResult as string}</div>
      </div>
    );
  }
  return '';
};

export const App: FC = () => {
  return (
    <div>
      <MessagesViewer selector={messagesSelector} actions={messageActions} formatter={messageFormatter} />
    </div>
  );
};

formatter - функция для кастомного отображения сообщения

dispatch(messageActions.add(Messages.error('Error', { details: {customDetails: ['customDetails']]}})))
dispatch(messageActions.add(Messages.success('Success')))
dispatch(messageActions.add(Messages.warning('Warning')))
dispatch(messageActions.add(Messages.info('Info')))

dispatch(messageActions.add({ title: 'Error', type: 'error', details: { body: 'error body'}})
dispatch(messageActions.add({ title: 'Success', type: 'success', delay: 1000, details: { body: 'success body'}})

dispatch(messageActions.remove(messageId);
dispatch(messageActions.clear();

```

# Toaster

<!-- description:start -->
Компонент позволяет показывать последние уведомления пользователя от системы.
Уведомление представляет собой сообщение со статусом и дополнительным перечнем действий,
которое пользователь может сделать с уведомлением.
<!-- description:end -->

## Пример использования

```ts
import React, { useState, useCallback } from 'react';
import { INotification, Toaster } from 'edu-components/Toaster/desktop';

const App = () => {
  const [notifications, changeNotifications] = useState<INotification[]>([]);

  const addNotification = useCallback(() => (
    changeNotifications(stateNotifications => (
      [...stateNotifications, {...notification, id: id++}]
    ))
  ), [changeNotifications]);
  const removeNotification = useCallback((id: INotification['id']) => (
    changeNotifications(stateNotifications => (
      stateNotifications.filter(notification => notification.id !== id)
    ))
  ), [changeNotifications]);

  return (
    <Toaster
      notifications={notifications}
      size={5}
      onClose={removeNotification}
    />
  );
);
```

## Свойства
<!-- props:start -->
| Свойство       | Тип                          | По умолчанию         | Описание                                         |
| -------------- | ---------------------------- | -------------------- | ------------------------------------------------ |
| animated?      | `false \| true`              | `false`              | Признак необходимости анимировать уведомления    |
| className?     | `string`                     | —                    | Класс компонента                                 |
| innerRef?      | `RefObject<HTMLDivElement>`  | —                    | Ссылка на корневой DOM-элемент компонента        |
| root?          | `Element`                    | `document.body`      | Контейнер компонента                             |
| size?          | `number`                     | `5`                  | Максимальное количество отображаемых уведомлений |
| notifications? | `INotification[]`            | `[]`                 | Список уведомлений                               |
| onClose        | `INotificationCloseCallback` | —                    | Обработчик закрытия уведомления                  |
| renderToast?   | `IRenderToastCallback`       | `<Toast {...props}>` | Функция рендера уведомления                      |
<!-- props:end -->|
, где `INotificationCloseCallback` — метод с типом `(id: INotification['id']): => void`, а `IRenderToastCallback` — метод с типом `(notification: INotification, onClose: INotificationCloseCallback) => ReactNode`

## INotification

| Свойство              | Тип                                | Значение по умолчанию | Описание                                                                                                     |
| --------------------- | ---------------------------------- | --------------------- | ------------------------------------------------------------------------------------------------------------ |
| `id`                  | `string | number`                  | —                     | Идентификатор уведомления                                                                                    |
| `status?`             | `'FAILURE' | 'SUCCESS'`            | —                     | Статус уведомления                                                                                           |
| `content`             | `ReactNode`                        | —                     | Контент уведомления                                                                                          |
| `autoclosable?`       | `boolean`                          | `false`               | Признак автоматического закрытия уведомления                                                                 |
| `autocloseTimeout?`   | `number`                           | `5000`                | Период времени автоматического закрытия уведомления                                                          |

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Toaster)

# События Мессенджера

## Пример подписки на события

```ts
widgetInstance.events.catchUrlClick.addListener(({ data }) => {
    openDeeplink(data.url);
});
```

## Доступные события

`ready`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>*

>Мессенджер готов для отображения

`close`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>*

>Клик по кнопке свернуть (крестик в шапке мессенджера)

`chatChange`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatChange](./interfaces.md#chatchange), void>>*

>Открытие чата

`chatLeave`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatLeave](./interfaces.md#chatleave), void>>*

>Закрытие/смена чата

`error`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[LegacyError](./interfaces.md#legacyerror), void>>*

>Ошибка

`locationChange`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[LocationChange](./interfaces.md#locationchange), void>>*

>Смена роута

`members`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[Members](./interfaces.md#members), void>>*

>Изменение количества участников чата

`unload`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>*

>Закрытие/перезагрузка страницы мессенджера

`messageSent`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[MessageSent](./interfaces.md#messagesent), void>>*

>Сообщение отправлено

`catchUrlClick`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[CatchUrlClick](./interfaces.md#catchurlclick), void>>*

>Клик по урлу (диплинку) хоста

`userNeedReAssign`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>*

>GUID пользователя мессенджера отличается от переданного в параметре requestedGuid

`userLoaded`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[UserLoaded](./interfaces.md#userloaded), void>>*

>Пользователь загружен

`chatHistoryLoaded`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatHistoryLoaded](./interfaces.md#chathistoryloaded), void>>*

>Отобразилась первая страница чата

`chatListLoaded`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>*

>Отобразился нулевой экран

`chatLoadError`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatLoadError](./interfaces.md#chatloaderror), void>>*

>Произошла ошибка загрузки чата

`fullscreenOn`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>*

>Открыть просмотр картинок в полноэкранном режиме

`fullscreenOff`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>*

>Выйти из полноэкранного режима просмотра картинок

`counter`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[Counter](./interfaces.md#counter), void>>*

>Изменилось кол-во непрочитанных сообщений

`unreadCountersByChats`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[UnreadCountersByChats](./interfaces.md#unreadcountersbychats), void>>*

>Изменилось кол-во непрочитанных сообщений в чатах переданных в флаге unreadCountersByChats

`channelSubscribed`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChannelSubscribed](./interfaces.md#channelsubscribed), void>>*

>Пользователь подписался на канал

`channelUnsubscribed`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChannelUnsubscribed](./interfaces.md#channelunsubscribed), void>>*

>Пользователь отписался от канала

`authRequest`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[AuthRequest](./interfaces.md#authrequest), void>>*

>Событие возникает при попытке авторизации в случае если authType=own

`sendMessage`: *[Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[SendMessage](./interfaces.md#sendmessage), void>>*

>Пользователь отправиляет сообщение (доставка не гарантируется)
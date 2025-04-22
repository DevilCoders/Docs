# Обработчики запросов из Мессенджера

Все возможные запросы из мессенджера собраны в `Widget::handlers`. Со стороны виджета
каждый запрос это событие, на которое можно подписаться с помощью `Event::addListener`.

Само событие это объект со следующими полями:

`response` - ответить на запрос, в качестве ответа можно передать промис.

`reject` - отклонить запрос

`payload` - параметры запроса

## Пример обработки запроса

```ts
widgetInstance.handlers.getLog.addListener(async (request) => {
    try {
        const logs = await fetchLogs();

        request.response(logs.map(log => new Blob([log])));
    } catch (error) {
        request.reject(error);
    }
});
```

## Доступные обработчики

`getLog`: *[Event](./interfaces.md#event)\<{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'getLog'

&nbsp;&nbsp;&nbsp;&nbsp;payload: unknown

&nbsp;&nbsp;&nbsp;&nbsp;response: (data: [MaybePromise](./interfaces.md#maybepromise)\<[GetLogResponse](./interfaces.md#getlogresponse) | Array\<Blob>>): void

&nbsp;&nbsp;&nbsp;&nbsp;reject: (error: Error): void

}>*

>Получить логи с хоста

`getEnv`: *[Event](./interfaces.md#event)\<{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'getEnv'

&nbsp;&nbsp;&nbsp;&nbsp;payload: unknown

&nbsp;&nbsp;&nbsp;&nbsp;response: (data: [MaybePromise](./interfaces.md#maybepromise)\<object>): void

&nbsp;&nbsp;&nbsp;&nbsp;reject: (error: Error): void

}>*

>Получить данные о хосте

`uiInterceptor`: *[Event](./interfaces.md#event)\<{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'uiInterceptor'

&nbsp;&nbsp;&nbsp;&nbsp;payload: [UiInterceptorParams](./interfaces.md#uiinterceptorparams)

&nbsp;&nbsp;&nbsp;&nbsp;response: (data: [MaybePromise](./interfaces.md#maybepromise)\<[UiInterceptorResponse](./interfaces.md#uiinterceptorresponse)>): void

&nbsp;&nbsp;&nbsp;&nbsp;reject: (error: Error): void

}>*

>Позволяет хосту выполнять свои действия вместо открытия стандартных интефейсов
Для включения необхоимо передать в мессенджер флаг uiInterceptor

>chat_info - перехват открытия панели информации о чате
user_info - перехват открытия панели информации о пользователе
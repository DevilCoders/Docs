# Описание внутреннего API для турбоаппа

В глобальном объекте доступен объект с внутренним API чекаута:
```ts
interface Window {
    yandexCheckoutInternalApi: YandexCheckoutInternalApi;
}

type YandexCheckoutInternalApi = {
    checkout: CheckoutApi;
    payments: PaymentsApi;
};
```

## CheckoutApi

```ts
type CheckoutApi = {
    // Получение объекта YandexCheckoutDetails, который магазин передал в конструктор YandexCheckoutRequest
    getCheckoutDetails(): Promise<YandexCheckoutDetails>;
    
    // Получение объекта YandexCheckoutOptions, который магазин передал в конструктор YandexCheckoutRequest
    getCheckoutOptions(): Promise<YandexCheckoutOptions | undefined>;

    // Кидает событие, которое обрабатывается на стороне магазина.
    // В ответ нужен промис, который резолвится после вызова всех обработчиков события на стороне магазина.
    // Если магазин вызвал метод `event.updateWith(details)`, то значением промиса будет `details` (может быть еще одним промисом).
    // Если магазин не вызывал `event.updateWith()` в обработчике события, то в значении промиса будет null.
    triggerEvent(name: string, state: YandexCheckoutState): Promise<Promise<YandexCheckoutDetailsUpdate> | YandexCheckoutDetailsUpdate | null>;

    // Добавление обработчика для событий контейнера.
    addEventListener(name: string, fn: () => void): void;

    // Удаление обработчика для событий контейнера.
    removeEventListener(name: string, fn: () => void): void;

    // Репортит высоту контента, чтобы контейнер подстроил свои размеры.
    setContentHeight(height: number): Promise<void>;
    
    // Проверить открыт ли контейнер в фулскрин режиме.
    isFullscreen(): Promise<boolean>;

    // Закрытие сплеш-скрина, когда форма готова к отображению.
    hideSplashScreen(): Promise<void>;
   
    // Закрытие формы после успешной оплаты.
    closeWithSuccess(state: YandexCheckoutState): void;
    
    // Закрытие формы с фатальной ошибкой. Завершает ошибкой промис из `YandexCheckoutRequest.show()`.
    // Параметр `name` проставляется в свойство ошибки `error.name`.
    // Вызывается, например, при отсутствии токена Яндекс Оплаты после события `paymentStart`. 
    closeWithError(name: string, message: string): void;

    // Информация о странице, с которой вызывается форма чекаута.
    getMerchantInfo(): Promise<{
        // Полный адрес страницы, с которого вызван чекаут 
        pageUrl: string;
        
        // Фавиконка страницы, с которой вызван чекаут
        favicon?: string;
    }>;
};
```

### События 

| Событие                                       | Когда вызывается                               | Зачем нужно                        |
| --------------------------------------------- | -----------------------------------------------| ---------------------------------- |
| `fullscreenchange(e: FullscreenChangeEvent)`  | При входе/выходе контейнера в fullscreen режим | Обновить layout с учетом фулскрина | 

```ts
interface FullscreenChangeEvent extends Event {
    isFullscreen: boolean;
}
```

## PaymentsApi

```ts
// Данные о способе оплаты
type PaymentMethod = {
    id: string; // Идентификатор способа оплаты
    type?: string; // Способ оплаты
    system?: string; // Платежная система
    number?: string; // Номер способа оплаты
};

type PaymentsApi = {
    // Получение способов оплаты
    getPaymentMethods(): Promise<Array<PaymentMethod>>;

    // Подготовка новой карты
    prepareCard(): Promise<PaymentMethod>;

    // Проведение платежа
    pay(payment_token: string, payment_method: PaymentMethod): Promise<void>;
};
```

### Обработка ошибок

#### prepareCard()
- `AbortError` - отмена добавления карты;

#### pay()
- `AbortError` - отмена оплаты;


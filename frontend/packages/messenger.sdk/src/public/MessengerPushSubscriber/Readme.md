# MessengerPushSubscriber

Модуль для работы с пушами мессенджера

На данный момент пакет не поддерживает работу с заблокированными куками. Т.е. работает только для [*.]yandex.{tld}

## Использование

```javascript
const {
    PostMessageTransport,
    MessengerPushSubscriber,
    createRegistryApi,
    subscriptionProviderFactory,
    REGISTRY_API_SCOPE,
} = require('@yandex-int/messenger.sdk/public');

// Создаем транспорт для registryApi
const postMessageTransport = new PostMessageTransport({
    iframeUrl: 'https://yandex.ru/chat/iframe-api',
    scopeParams: {
        [REGISTRY_API_SCOPE]: {
            // Параметры, подробнее в https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/messenger/packages/sdk/src/publicApi/registry-api/Readme.md#L5
        }
    }
});

// Создаем registryApi для запросов в бекенд
const registryApi = createRegistryApi(postMessageTransport);

// Создаем провайдер подписки
const subscriptionProvider = subscriptionProviderFactory(() => {
    // Получаем регистрацию сервис воркера
    const swRegistration = getSWRegistration();

    return swRegistration;
});

const messengerPushSubscriber = new MessengerPushSubscriber(
    registryApi,
    subscriptionProvider,
);

//...

// Подписка на пуши мессенджера
const { logout_token } = await messengerPushSubscriber.subscribe({
    uuid: string // Уникальный айди подписки
    deviceId: string // Айди устройства, можно сгенерировать с помощью @yandex-int/messenger.sdk#createUUID
    workspaceId?: number // Айди сервиса
});

// ...

// Отписка от пушей
await messengerPushSubscriber.unsubscribe(logout_token);
```


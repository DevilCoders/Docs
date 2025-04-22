# RegistryApi

Клиент для использования методов бекенда `registryApi` мессенджера.

## Параметры RegistryApi

| Название | Описание |
| -------- | -------- |
| `workspaceId?` | Айди воркспейса |
| `oauthToken?` | Токен авторизации |
| `serviceId?` | Айди сервиса |


## Использование

```javascript
const { PostMessageTransport, createRegistryApi, REGISTRY_API_SCOPE } = require('@yandex-int/messenger.sdk');

const postMessageTransport = new PostMessageTransport({
    iframeUrl: 'https://yandex.ru/chat/iframe-api',
    scopeParams: {
        [REGISTRY_API_SCOPE]: {
            // Параметры
        }
    }
});
const api = createRegistryApi(postMessageTransport);

const vapid = await api.getVapid();

//...

const { logout_token } = await api.setPushToken(...params);

// ...

await api.revokePushToken(logout_token);
```

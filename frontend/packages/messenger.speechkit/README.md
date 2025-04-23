# messenger.speechkit

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.speechkit/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.speechkit)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.speechkit)<br>
[![dep health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.speechkit)](https://oko.yandex-team.ru/pkg/@yandex-int/messenger.speechkit)

## Установка

### Пакеты

```
npm i --save @yandex-int/messenger.websocket @yandex-int/messenger/uniproxy @yandex-int/messenger/speechkit
```

### Подключение
```ts
import { WebSocketTransport } from '@yandex-int/messenger.websocket';
import { Uniproxy } from '@yandex-int/messenger.uniproxy';
import {
    vinsRequestFactoryProvider,
    Speechkit,
    UniproxyConfig,
    UniproxySpeechkitService,
} from '@yandex-int/messenger.speechkit';

// Не использовать apiKey, url, appId мессенджера в продакшене!!!
const config = new UniproxyConfig({
    apiKey: '069b6659-984b-4c5f-880e-aaedcfd84102',
    url: 'wss://uniproxy.messenger.yandex.ru/uni.ws',
    suspendable: true,
});

const websocket = new WebSocketTransport();

websocket.setup(config.getUrl());

const uniproxy = new Uniproxy(websocket);
const uniproxySpeechkitService = new UniproxySpeechkitService(uniproxy, config);

const speechkit = new Speechkit(
    uniproxySpeechkitService,
    vinsRequestFactoryProvider({
        uuid: 'some_test_uuid2',
        appId: 'ru.yandex.messenger',
        appVersion: '1.0.1',
        platform: navigator.platform,
        osVestion: navigator.userAgent,
        vinsTopic: 'desktopgeneral',
        experiments: ['multi_tabs', 'find_poi_gallery', 'find_poi_one'],
        timezone: 'Europe/Moscow',
    }),
);

(window as any).__speechkit = speechkit;
```

Описание событий и ручек находится в классе `Speechkit`

### Промисификация
Для промисификация запрос можно использовать модуль `RequestsBucket` (входит в состав пакета)
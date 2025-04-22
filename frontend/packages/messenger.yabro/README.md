# @yandex-int/messenger.yabro

[![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.yabro/version.svg)](https://npm.yandex-team.ru/-/ui/?text=@yandex-int/messenger.yabro)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.yabro)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.yabro)<br>
[![dist health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.yabro)](https://oko.yandex-team.ru/pkg/@yandex-int/messenger.yabro)

Пакет для работы с нативными модулями Ябро.

Все проксируемые события и методы, а так же сам инстанс прокси поддерживают флаг notSupported.

## Messenger

Создает безопасную прокси для yandex.messenger.

```typescript
import { createMessengerApi } from '@yandex-int/messenger.yabro';

const nativeApi = createMessengerApi();

nativeApi.openView(chatLink);
```

## Experiments

Создает безопасную прокси для yandex.experiments.

```typescript
import { createExperimentsApi } from '@yandex-int/messenger.yabro';

export const experimentsApi = createExperimentsApi<ExperimentsNames>();

if (!experimentsApi.getAll.notSupported) {
  experimentsApi.getAll(callback);
}

if (!experimentsApi.getValue.notSupported) {
  experimentsApi.getValue(name, callback);
}

```

А так же 2 хэлпера для поиска и получения экспериментов:

```typescript
import { findExperiment, getExperiment } from '@yandex-int/messenger.yabro';

experimentsApi.getAll((experiments) => {
  findExperiment(experiments, name);
});

getExperiment('mssng').then((exp) => {});
```

## Statistics

Создает безопасную прокси для yandex.statistics.

```typescript
import { createStatisticsApi } from '@yandex-int/messenger.yabro';

export const NativeStatisticsApi = createStatisticsApi();

NativeStatisticsApi.send(client_id, data);
```

## Sound

Создает безопасную прокси для yandex.sound.

```typescript
import { createSoundApi } from '@yandex-int/messenger.yabro';

const soundApi = createSoundApi();

if (!soundApi.playPushNotificationSound.notSupported) {
  soundApi.playPushNotificationSound(sound);
}
```

## DeepSync

Создает безопасную прокси для yandex.deepSync.

```typescript
import { createDeepSyncApi } from '@yandex-int/messenger.yabro';

const deepSyncApi = createDeepSyncApi();

deepSyncApi.loadComplete();
```

## NativeTransportIframeClient

Модуль позволяет отправлять/получать сообщения Ябро хосту находящемуся не на yandex.ru.

Для работы модуль создает айфрейм который находится на yandex.ru, в айфрейме запускается код который проксирует входящие сообщения к ябро и обратно.

### tl;dr

```typescript
import { NativeTransportIframeClient } from '@yandex-int/messenger.yabro';

const client = new NativeTransportIframeClient({
    iframeUrl: 'https://yandex.ru/chat/native-transport',
});

const openBalloonHandler = () => {
    client.showChat({ chatId: '1/2/e7c13556-8ed7-4b97-b4cd-569f6541b1b6' });
};

deleteIframeBtn.addEventListener('click', () => {
    openBalloonBtn.removeEventListener('click', openBalloonHandler);
    client.destroy();
});

createIframeBtn.addEventListener('click', () => {
    client.create({
        onReady() {
            openBalloonBtn.addEventListener('click', openBalloonHandler);
        },
        onError() {

        }
    });
});
```

### Использование

Импортируем клиент из пакета:

```typescript
import { NativeTransportIframeClient } from '@yandex-int/messenger.yabro';
```

Далее создаем экземпляр клиента, передав в него адрес на котором находится код айфрейма:

```typescript
const client = new NativeTransportIframeClient({
    iframeUrl: 'https://yandex.ru/chat/native-transport',
});
```

У клиента есть 3 метода: `create, showChat и destroy`

#### create

```typescript
client.create({
    onReady() {
        // Браузер подходит для открытия нативного балуна мессенджера и готов это сделать, можно вызывать client.showChat({...})
    },
    onError() {
        // Либо произошла ошибка загрузки, либо браузер не подходит для открытия нативного балуна мессенджера
    }
});
```

Создает айфрейм, получает от него событие `ready` или `error` и вызывает соответствующие методы у адаптера.

#### showChat

Параметры:
(Параметры совпадают с аналогичным методом у [виджета](https://github.yandex-team.ru/serp/chat/blob/dev/services/widget-loader/docs/widget_ya.md#свойства-и-методы))

```typescript
{
    guid?: string;
    chatList?: boolean;
    chatId?: string;
    pasteText?: string;
    chatMetadata?: {
        calls?: {
            video: 'init_on' | 'init_off' | 'force_on' | 'force_off' | 'default';
            microphone: 'init_on' | 'init_off' | 'force_on' | 'force_off' | 'default';
            may_call: boolean;
            skip_feedback: boolean
        };
        chatbar?: {
            video: 'init_on' | 'init_off' | 'force_on' | 'force_off' | 'default';
            microphone: 'init_on' | 'init_off' | 'force_on' | 'force_off' | 'default';
            may_call: boolean;
            skip_feedback: boolean
        };
    };
    pasteForce?: boolean;
    initCall?: 'audio' | 'video';
}
```

Открывает нативный балун ябро с переданными параметрами.

#### destroy

Удаляет айфрейм и очищает переменные

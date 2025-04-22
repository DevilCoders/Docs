# @yandex-int/messenger.channels

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.channels/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.channels)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.channels)<br>
[![dep health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.channels)](https://oko.yandex-team.ru/pkg/@yandex-int/messenger.channels)

## About:

Library for transmitting messages between windows, frames, workers or even websockets with support of requests/response, events, and observers.

## Install:

```
npm i @yandex-int/messenger.channels --registry=http://npm.yandex-team.ru
```

## Usage:

```
// host-api.ts

interface Requests {
    ping(): 'ok';
}

interface Events {
    iamalive: { message: string; };
}

interface Observers {
    state: { counter: number };
}

// iframe-api.ts

interface Requests {
    howMachMoneyDoYouHave(): number;
}

interface Events {
    iamalive: { message: string; };
}

interface Observables {
    state: { counter: number };
}

// host.ts
import { IframePostMessageTransport, ChannelOutgoing, channelMessagesHandlerFactory, channelProxyFactory } from '@yandex-int/messenger.channels';
import * as IframeApi from './iframe-api.ts';
import * as HostApi from './host-api.ts';

const transport = new IframePostMessageTransport(
    document.getElementById<HTMLIFrameElement>('some-iframe').contentWindow,
    'https://iframe.ru',
    ['https://iframe.ru'],
);

const channel = new ChannelOutgoing<
    IframeApi.Requests,
    HostApi.Requests,
    IframeApi.Events,
    HostApi.Events,
    HostApi.Observers,
    {},
    { someScope: { secret: string; } }
>
    ('myChannel', transport, {
        someScope: {
            secret: 'some-secret-key',
        },
    });

const requests = channelProxyFactory<HostApi.Requests>('someScope', channel, ['ping']);
const handler = channelMessagesHandlerFactory('someScope', () => {
    return {
        howMachMoneyDoYouHave() {
            return Math.round(Math.random() * 100);
        },
    };
});

channel.onConnectionEstablished.addListener(handler.onInit);
channel.onMessage.addListener(handler.onEvent);

channel.onEvent.addListener((event) => {
    console.log(event.type, event.data);
});

channel.observe('state', (newState) => {
    console.log('state was changed', newState);
});

requests.ping()
    .then((response) => {
        console.log('pong', response);
    });

// iframe.ts
import { WindowPostMessageTransport, ChannelIncoming } from '@yandex-int/messenger.channels';
import * as IframeApi from './iframe-api.ts';
import * as HostApi from './host-api.ts';

const state = {
    counter: 0;
}

const transport = new IframePostMessageTransport(
    window,
    'https://hostname.ru',
    ['https://hostname.ru'],
);

const channel = new ChannelIncoming<
    HostApi.Requests,
    IframeApi.Requests,
    HostApi.Events,
    IframeApi.Events,
    {},
    HostApi.Observables,
    { someScope: { secret: string; } },
>
    ('myChannel', transport);

const requests = channelProxyFactory<HostApi.Requests>('someScope', channel, ['howMachMoneyDoYouHave']);
const handler = channelMessagesHandlerFactory('someScope', ({ secret }) => {
    return {
        ping() {
            if (secret !== 'some-secret-key') {
                throw new Error('Bad secret');
            }

            return 'ok';
        },
    };
});

channel.onConnectionEstablished.addListener(handler.onInit);
channel.onMessage.addListener(handler.onEvent);

channel.onEvent.addListener((event) => {
    console.log(event.type, event.data);
});

channel.onObserve.addEventListener((event) => {
    if (event.data.objectName === 'state') {
        event.notify(state);
    }
});

requests.howMachMoneyDoYouHave()
    .then((response) => {
        console.log('Host have', response);
    });

function updateCounter(value: number) {
    state.counter = value;

    channel.notifyObservers('state', state);
}
```
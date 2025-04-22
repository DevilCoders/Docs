# Быстрое введение в работу оверлея

Это введение не является полным, но содержит в себе примеры для быстрого внедрения.

Более подробно обо всем, что умеет оверлей можно прочитать в [api reference](./api.md).

## Добавляем оверлей на страницу:
Для того, чтобы **просто** открыть оверлей нужно сделать всего три вещи:

1. Добавить скрипт с оверлеем на страницу, https://yastatic.net/s3/turbo-static/overlay/v1.2.0/overlay.js

2. Убедиться, что скрипт загрузился:
- `script.onload`
- `window.Ya.turboOverlayLoaded = function() {}`

3. Вызвать метод `window.Ya.turboOverlay.open(config)`

Самый просто вариант (и что-то подобное у нас уже есть для [тестирования](https://github.yandex-team.ru/serp/turbo/blob/dev/.templar/plugins/controllers/overlay/overlay.html)):

*Такой код будет работать:*
```js
window.Ya = window.Ya || {};

window.Ya.turboOverlayLoaded = () => {
    document.addEventListener('click', e => {
        if (!e.target || e.target.tagName.toLowerCase() !== 'a') {
            return;
        }
        window.Ya.turboOverlay.open({
            urls: [{
                // ссылка на турбо-страницу: iframe src
                frameUrl: e.target.getAttribute('href'),

                // ссылка, которую увидит пользователь
                displayUrl: e.target.getAttribute('data-display-url'),

                // ссылка, на которую произойдет редирект при ошибке
                originalUrl: e.target.getAttribute('data-original-url'),
            }],
        });
        e.preventDefault();
    });
};

const script = document.createElement('script');
script.src = 'https://yastatic.net/s3/turbo-static/overlay/v1.2.0/overlay.js';

document.head.appendChild(script);
```
*Для ссылок:*
```html
<a
  href="https://yandex.ru/turbo?text=text=https%3A%2F%2Frsport.ria.ru%2F20190813%2F1557469930.html&parent-reqid=100&trbsrc=wb"
  data-display-url="/turbo?text=text=https%3A%2F%2Frsport.ria.ru%2F20190813%2F1557469930.html"
  data-original-url="https://rsport.ria.ru/20190813/1557469930.html"
>
  турбо-ссылка на https://rsport.ria.ru/20190813/1557469930.html
</a>
```

> `displayUrl` лучше делать относительным, турбо-урл `frameUrl` **нужно** делать абсолютным.

После этого может произойти одно из двух (немного позже мы будем менять это поведение):

### Турбо работает корректно:

1. В истории появится новая запись: `history.pushState`, урл изменится на турбовый, например на `/turbo?text=…` или `/pogoda/`, так, чтобы если пользователь перезагрузил страницу, то попал на турбо-страницу без оверлея.
2. Показалось тело (белое) оверлея и отрисовался спикер
3. После загрузки оверлея пользователь увидит турло-страницу

### Произошел fallback, ошибка сети (`iframe.onerror`), или прошло 5 секунд, но страница не загрузилась:

1. В истории появится новая запись: `history.pushState`, урл изменится на турбовый, например на `/turbo?text=…` или `/pogoda/`, так, чтобы если пользователь перезагрузил страницу, то попал на турбо-страницу без оверлея.
2. Покажется тело (белое) оверлея и отрисуется спикер
3. Произошла перезагрузка на оригинал:

- страница паблишера (e.g. https://ria.ru)
- страница сервиса, которая может работать без турбо (e.g. https://yandex.ru/pogoda?no_turbo-1)

## Отправляем базовые счетчики и блокируем скролл
По умолчанию оверлей скролл не скрывает, т.к. считает это сервисоспецифичным.

Предполагается, что большинство сервисов имеет готовый для этого код.
Если такого кода нет, то можно воспользоваться библиотекой [body-scroll-lock](https://www.npmjs.com/package/body-scroll-lock) с достаточно коротким [исходным кодом](https://github.com/willmcpo/body-scroll-lock/blob/master/src/bodyScrollLock.js), которая используется внутри самого турбо. [body-scroll-lock на bundlephobia](https://bundlephobia.com/result?p=body-scroll-lock@2.6.4). Ее и будем использовать в примере.

```js
window.Ya = window.Ya || {};
window.Ya.turboOverlayLoaded = () => {
    document.addEventListener('click', e => {
        if (!e.target || e.target.tagName.toLowerCase() !== 'a') {
            return;
        }

        window.Ya.turboOverlay.open({
            urls: [{
                // ссылка на турбо-страницу: iframe src
                frameUrl: e.target.getAttribute('href'),

                // ссылка, которую увидит пользователь
                displayUrl: e.target.getAttribute('data-display-url'),

                // ссылка, на которую произойдет редирект при ошибке
                originalUrl: e.target.getAttribute('data-original-url'),
            }],
        });

        e.preventDefault();
    });
};

const script = document.createElement('script');
script.src = 'https://yastatic.net/s3/turbo-static/overlay/v1.2.0/overlay.js';

document.head.appendChild(script);

window.Ya.turboOverlay.onOverlayOpen = ({ root }) => {
    bodyScrollLock.disableBodyScroll(root);
};

window.Ya.turboOverlay.onOverlayClose = ({ root }) => {
    bodyScrollLock.enableBodyScroll(root);
};
```

Первая функция вызывается при открытии оверлея, вторая при его закрытии, (возврате назад).

Cюда же можно добавить счетчики аналитики.

Оверлей не делает это самостоятельно, так как также предполагает это сервисоспецифичным. Предположим, что у вас есть функция `sendCounter`. Тогда предыдущий пример можно преобразовать в:

```js
window.Ya = window.Ya || {};

window.Ya.turboOverlayLoaded = () => {
    document.addEventListener('click', e => {
        if (!e.target || e.target.tagName.toLowerCase() !== 'a') {
            return;
        }

        window.Ya.turboOverlay.open({
            urls: [{
                // ссылка на турбо-страницу: iframe src
                frameUrl: e.target.getAttribute('href'),

                // ссылка, которую увидит пользователь
                displayUrl: e.target.getAttribute('data-display-url'),

                // ссылка, на которую произойдет редирект при ошибке
                originalUrl: e.target.getAttribute('data-original-url'),
            }],

        });

        e.preventDefault();
    });
};

const script = document.createElement('script');
script.src = 'https://yastatic.net/s3/turbo-static/overlay/v1.1.0/overlay.js';

document.head.appendChild(script);

window.Ya.turboOverlay.onOverlayOpen = ({ root }) => {
    bodyScrollLock.disableBodyScroll(root);
    sendCounter(['690.2719.2815']); // /tech/turbo/try_open
};

window.Ya.turboOverlay.onOverlayClose = ({ root }) => {
    bodyScrollLock.enableBodyScroll(root);
    sendCounter(['80.22.2719.2242.221']); // /web/item/turbo/sideblock/back
};
```

## Отправляем информацию о фолбэках:

Фолбэки на оригинал — способ турбо подложить соломку в случае поломок. Есть (возможно немного устаревшее) исследование от @gfranco [Фолбэки турбо](https://wiki.yandex-team.ru/turbo/fallback/), в частности там описано, что может пойти не так: [Причины фолбэков](https://wiki.yandex-team.ru/turbo/fallback/#prichinyfolbekov).

Оверлей разделяет и позволяет обработать все виды фолбэков, передавая информацию о них в параметрах. Разные варианты падений могут свидетельствовать о разных поломках в продакшине.

```js
window.Ya = window.Ya || {};

window.Ya.turboOverlayLoaded = () => {
    document.addEventListener('click', e => {
        if (!e.target || e.target.tagName.toLowerCase() !== 'a') {
            return;
        }

        window.Ya.turboOverlay.open({
            urls: [{
                // ссылка на турбо-страницу: iframe src
                frameUrl: e.target.getAttribute('href'),

                // ссылка, которую увидит пользователь
                displayUrl: e.target.getAttribute('data-display-url'),

                // ссылка, на которую произойдет редирект при ошибке
                originalUrl: e.target.getAttribute('data-original-url'),
            }],
        });

        e.preventDefault();
    });
};

const script = document.createElement('script');

script.src = 'https://yastatic.net/s3/turbo-static/overlay/v1.1.0/overlay.js';

document.head.appendChild(script);

window.Ya.turboOverlay.onOverlayOpen = ({ root }) => {
    bodyScrollLock.disableBodyScroll(root);
    sendCounter(['690.2719.2815']); // /tech/turbo/try_open
};

window.Ya.turboOverlay.onOverlayClose = ({ root }) => {
    bodyScrollLock.enableBodyScroll(root);
    sendCounter(['80.22.2719.2242.221']); // /web/item/turbo/sideblock/back
};

window.Ya.turboOverlay.onOverlayFallback = ({ fallbackType }) => {
    switch (fallbackType) {
        case 'timeout':
            this._sendCounter(['690.2719.2010.2922']); // /tech/turbo/fallback/timeout
            break;

        case 'frameError':
            this._sendCounter(['690.2719.3513']); // /tech/turbo/frame-error;
            break;

        case 'message':
            this._sendCounter(['690.2719.2010.3731']); // /tech/turbo/fallback/nodata
            break;
    }
};
```



# Кастомизируем оверлей
Вероятнее всего, “просто оверлей” не будет работать так, как нужно вам, поэтому вам захочется его кастомизировать:



## Внешний вид:
Оверлей можно стилизовать через `css`. Он добавляет css инлайном в head, соответственно любой css добавленный в `body` будет выше по специфичности.

В случае, если стили внешние, то их можно перебить специфичностью, например, через селектор атрибута `class`

```css
[class].turbo-overlay {
    color: #000;
}
```

В будущем предполагается api полной замены шапки, но на текущий момент оно не имплементировано:

`window.Ya.turboOverlay.updateHead(() => HTMLElement)`

## Кастомизация истории:
Сейчас при открытии оверлея урл изменится на турбированный, например `https://yandex.ru/turbo?text=about`. В ряде случаев это нежелаемо (не хочется уводить пользователя с сервиса при перезагрузке страницы) или просто не будет работать (поддомены).



### ВАЖНО
При создании своих урлов необходимо учитывать, что оверлей можно открыть только на урле, из которого можно восстановить турбо-ссылку, напрямую, либо через query-параметр.

Т.е. такие урлы **можно** использовать:

- `https://yandex.ru/turbo?text=test_news`
- `https://service.yandex.ru/some/path?q=https%3A%2F%2Fyandex.ru%2Fturbo%3Ftext%3Dabout`

А такой урл использовать **нельзя**:
- `https://yandex.ru/ololo?q=1&a=2`

Это связано с браузерными багами истории ([оверелей и история](./history)).

### Используем хуки для создания нужных ссылок:
Предположим, у нас есть сервис `ololo`, живущий не на едином домене, `servie.yandex.{tld}`.

Во-первых, нам очевидно нужно будет заменить ссылки при открытии на такие, которые нас бы устраивали. В нашем случае это будут:

Для этого мы изменим data-display-url и ссылка из первого примера будет выглядеть так:

```html
<a
  href="https://yandex.ru/turbo?text=text=https%3A%2F%2Frsport.ria.ru%2F20190813%2F1557469930.html&parent-reqid=100&trbsrc=wb"
  data-display-url="/sidebar?q=https%3A%2F%2Frsport.ria.ru%2F20190813%2F1557469930.html"
  data-original-url="https://rsport.ria.ru/20190813/1557469930.html"
>
  турбо-ссылка на https://rsport.ria.ru/20190813/1557469930.html
</a>
```

Проблема в том, что такая ссылка проживет недолго, вплоть до загрузки страницы. Сразу после того, как страница загрузится оверлей изменит урл на тот, который она отправила.

Давайте добавим хуков, чтобы все ссылки были “правильными”.
```js
window.Ya = window.Ya || {};

window.Ya.turboOverlayLoaded = () => {
    document.addEventListener('click', e => {
        if (!e.target || e.target.tagName.toLowerCase() !== 'a') {
            return;
        }

        window.Ya.turboOverlay.open({
            urls: [{
                // ссылка на турбо-страницу: iframe src
                frameUrl: e.target.getAttribute('href'),

                // ссылка, которую увидит пользователь
                displayUrl: e.target.getAttribute('data-display-url'),

                // ссылка, на которую произойдет редирект при ошибке
                originalUrl: e.target.getAttribute('data-original-url'),
            }],
        });

        e.preventDefault();
    });
};

const navigate = ({ to }) => ({
    displayUrl: `https://ololo.yandex.ru/sidebar?q=${encodeURIComponent(to)}`,
});

const show = ({ displayUrl }) => ({
    displayUrl: `https://ololo.yandex.ru/sidebar?q=${encodeURIComponent(displayUrl)}`,
});

/* фунцкии навигации */

window.Ya.turboOverlay = {
    ...window.Ya.turboOverlay,

    onOverlayNavigate: navigate,
    onOverlayRelocate: navigate,
    onOverlayNewFrameOpened: navigate,

    onOverlayContentShown: show,
    onOverlayActiveDocumentChanged: show,

    onOverlayFallback: ({ fallbackType }) => {
        switch (fallbackType) {
            case 'timeout':
                this._sendCounter(['690.2719.2010.2922']); // /tech/turbo/fallback/timeout
                break;

            case 'frameError':
                this._sendCounter(['690.2719.3513']); // /tech/turbo/frame-error;
                break;

            case 'message':
                this._sendCounter(['690.2719.2010.3731']); // /tech/turbo/fallback/nodata
                break;
        }
    },

    onOverlayOpen: ({ root }) => {
        bodyScrollLock.disableBodyScroll(root);
        sendCounter(['690.2719.2815']); // /tech/turbo/try_open
    },

    onOverlayClose: ({ root }) => {
        bodyScrollLock.enableBodyScroll(root);
        sendCounter(['80.22.2719.2242.221']); // /web/item/turbo/sideblock/back
    },
};

const script = document.createElement('script');
script.src = 'https://yastatic.net/s3/turbo-static/overlay/v1.1.0/overlay.js';
document.head.appendChild(script);
```

Оверлей умеет еще кое-что, но это выходит за пределы быстрого старта:
- [api-reference](./api.md)
- [palmsync —  пользовательские сценарии](../__tests__/overlay.testpalm.yml)

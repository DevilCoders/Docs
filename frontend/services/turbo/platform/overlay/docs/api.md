
# Api оверлея

> Примечание:
Api находятся внутри неймспейса `window.Ya.turboOverlay`, но для простоты он не указывается напрямую в описании методов (но указывается в примере).
Вне неймспейса существует только хук `window.Ya.turboOverlayLoaded`, который может вызываться до инициализации неймспейса.

1. [Публичные функции](#публичные-функции), которые должен вызывать сам сервис для управления оверлеем:
    - [`open`](#open)
    - [`close`](#close)
    - [`isOpen`](#open)
    - [`showCloseButton`](#showclosebutton)
    - [`hideCloseButton`](#hideclosebutton)
    - [`showNextPage`](#shownextpage)
    - [`showPrevPage`](#showprevpage)
2.  [lifecycle hooks](#lifecycle-hooks), которые будет вызывать сам оверлей и в зависимости от возвращаемого значения модифицировать свое поведение:
    - [`onOverlayOpen`](#onoverlayopen)
    - [`onOverlayClose`](#onoverlayclose)
    - [`onOverlayContentShown`](#onoverlaycontentshown)
    - [`onOverlayFallback`](#onoverlayfallback)
    - [`onOverlayNavigate`](#onoverlaynavigate)
    - [`onOverlayNewFrameOpened`](#onoverlaynewframeopened)
    - [`onOverlayRelocate`](#onoverlayrelocate)
    - [`onOverlayActiveDocumentChanged`](#onoverlayactivedocumentchanged)
    - [`onOverlayHeaderHidden`](#onoverlayheaderhidden)
    - [`onOverlayHeaderVisible`](#onoverlayheadervisible)
    - [`onOverlayCloseButtonClick`](#onoverlayclosebuttonclick)
    - [`onOverlayBackButtonClick`](#onoverlaybackbuttonclick)
    - [`onOverlayBrokenHistoryRecord`](#onoverlaybrokenhistoryrecord)
    - [`onOverlayPageChanged`](#onoverlaypagechanged)



## Публичные функции

- [`open`](#open)
- [`close`](#close)
- [`isOpen`](#open)
- [`showCloseButton`](#showclosebutton)
- [`hideCloseButton`](#hideclosebutton)
- [`showNextPage`](#shownextpage)
- [`showPrevPage`](#showprevpage)

### `open`
```ts
function open(config: IConfig, updateHistoryState: boolean = true): void;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

/** набор данных для открытия простого оверлея */
export interface IConfig {
    /** набор урлов, которые ведут на правильную страницу */
    urls: IOpenData[];
    /** позиция слайда из urls, который должен быть выведен (в случае мультислайдера) */
    index?: number;
    /** мета-информация для простоты работы с хуками */
    meta?: AnyJson;
    /** тайтл, который можно опционально нарисовать в оверлее */
    title?:  string;
    /** нужно ли открывать приложение в супераппе, если оно существует для турбо-страницы */
    openTurboApp?: boolean;
}

export interface IOpenData {
    /** урл, с которым будет открыт оверлей */
    frameUrl: string;
    /** урл, который будет необходимо отобразить в адресной строке */
    displayUrl: string;
    /** оригинальный урл страницы для редиректа при фолбэке */
    originalUrl: string;
    /**
     * Нужен для корректной работы аналитики в метрике для паблишеров,
     * записывается в атрибут data-sc-host.
     * @see https://st.yandex-team.ru/SERP-85995
     */
    hostForMetrika?: string;
}
```
Открывает оверлей с указанными параметрами.  Первым параметром ему передается конфиг для открытия, вторым — нужно ли добавлять запись в истории.

Если в параметре `urls` передано более одного элемента, откроется мультислайдер.
https://jing.yandex-team.ru/files/al88/1-1.png

В случае, если домен в displayUrl отличается от текущего домена на странице (бывает, например, в тестовых окружениях), вместо displayUrl в историю будет добавлен текущий url. Если так не делать, history api запретит добавление другого домена в историю и при возврате назад мы окажемся на странице, предшествующей той, с которой открывался турбо.

Параметр `meta` в конфиге открытия записывается в историю, поэтому не может содержать несериализуемых структур данных (например, функций или классов). В него удобно передавать, например, счетчики, которые будут вызываться при открытии и закрытии оверлея.

Это позволит отсылать их даже в том случае, если пользователь перезагрузил страницу (и потерян текущий контекст приложения). Туда же можно передавать детали состояния, чтобы не хранить его в хуках.

Модифицировать его после открытия будет нельзя.

Параметром `title` в конфиге можно отрисовать текст в шапке сайдбара, при этом надпись "назад" скроется:
https://jing.yandex-team.ru/files/werreour/20190830151925.jpg

В случае открытия мультислайдера `title` будет выведен над точками. Если `title` не передан, на его месте будет выводиться хост из оригинального урла текущей открытой страницы, если хосты одинаковые. В случае, когда переданные хосты разные,
над точками будут выводиться все имена хостов и прокручиваться к текущему хосту.

Параметр `openTurboApp` в конфиге управляет открытием урла в суппераппе. Если передано значение `true` и если для данного урла существует зарегистрированный турбо-апп, урл откроется в этом турбо-аппе. Проверка проиходит матчингом с `base_url` из манифеста. Параметр, необязательный, по умолчанию `true`.

Если второй параметр `false`, то будет сделан `history.replaceState`, в ином случае `history.pushState`.

```ts
// базовое использование
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

/*
 * => в браузерной истории появляется новая запись, урл меняется на /turbo?text=https://kp.ru
 * => в dom добавляется iframe с src https://yandex.ru/turbo?text=https://kp.ru, показывается спиннер
 * ...
 */

// открытие без записи в истории (восстановление оверлея после перезагрузки страницы)
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
}, false);

/*
 * => урл меняется на /turbo?text=https://kp.ru
 * => в dom добавляется iframe с src https://yandex.ru/turbo?text=https://kp.ru, показывается спиннер
 * ...
 */

// открытие с тайтлом
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
    title: 'Новости'
});

/*
 * Оверлей открывается с тайтлом:
 * https://jing.yandex-team.ru/files/werreour/20190830151925.jpg
 */

// мультислайдер
window.Ya.turboOverlay.open({
    urls: [
        {
            frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
            displayUrl: '/turbo?text=https://kp.ru',
            originlUrl: 'https://kp.ru',
        },
        {
            frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
            displayUrl: '/turbo?text=https://kp.ru',
            originlUrl: 'https://kp.ru',
        },
    ],
});

```

### `close`
```typescript
function close(): void;
```

Закрывает оверлей через `history.go()` (учитывает все переходы турбо-в-турбо).
```ts
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
});
// => открылся оверлей
window.Ya.turboOverlay.close()
// => оверлей закрылся,вне зависимости, как глубоко был пользователь на переходах турбо-в-турбо

window.Ya.turboOverlay.close()
// => ничего не происходит, оверлей уже закрыт
```

### `isOpen`
```typescript
function isOpen(): boolean;
```
Возвращает `true`, если оверлей сейчас открыт.

```ts
window.Ya.turboOverlay.isOpen(); // false

window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

window.Ya.turboOverlay.isOpen(); // true
window.Ya.turboOverlay.close();
window.Ya.turboOverlay.isOpen(); // false
```

### `showCloseButton`
```typescript
function showCloseButton(): void;
```
Показывает крестик справа в шапке:
https://jing.yandex-team.ru/files/werreour/20190901004202.png

При клике по нему оверлей закроется учитывая все переходы турбо-в-турбо.  Восстанавливается из истории при повторном открытии оверлея после шага назад.

```ts
window.Ya.turboOverlay.showCloseButton();

// открывается с крестиком
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

history.back()
// => оверлей закрылся
history.forward()
// => оверлей открылся с крестиком
```

### `hideCloseButton`
```typescript
function hideCloseButton(): void;
```
Скрывает крестик справа в шапке:
https://jing.yandex-team.ru/files/werreour/20190901004202.png

При клике по нему оверлей закроется учитывая все переходы турбо-в-турбо.  Восстанавливается из истории при повторном открытии оверлея после шага назад.

```ts
window.Ya.turboOverlay.showCloseButton();

// открывается с крестиком
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

// убирает крестик, оверлей откроется без него
window.Ya.turboOverlay.hideClosButton();

history.back()
// => оверлей закрылся
history.forward()
// => оверлей открылся без крестика
```

### `showNextPage`
```typescript
function showNextPage(): void;
```
Выполняет переход к следующей странице в режиме мультислайдера.

```ts
// открывается в режиме мультислайдера, активна первая страница
window.Ya.turboOverlay.open({
    urls: [
        {
            frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
            displayUrl: '/turbo?text=https://kp.ru',
            originlUrl: 'https://kp.ru',
        },
        {
            frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
            displayUrl: '/turbo?text=https://kp.ru',
            originlUrl: 'https://kp.ru',
        },
    ],
    index: 0,
});

window.Ya.turboOverlay.showNextPage();
// => происходит переход ко второй странице
```

### `showPrevPage`
```typescript
function showPrevPage(): void;
```
Выполняет переход к предыдущей странице в режиме мультислайдера.

```ts
// открывается в режиме мультислайдера, активна вторая страница
window.Ya.turboOverlay.open({
    urls: [
        {
            frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
            displayUrl: '/turbo?text=https://kp.ru',
            originlUrl: 'https://kp.ru',
        },
        {
            frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
            displayUrl: '/turbo?text=https://kp.ru',
            originlUrl: 'https://kp.ru',
        },
    ],
    index: 1,
});

window.Ya.turboOverlay.showPrevPage();
// => происходит переход к первой странице
```

## Lifecycle hooks

В процессе работы оверлей вызывает функции из глобального объекта `window.Ya.turboOverlay`, результат выполнения которых может влиять на его поведение.

Можно вернуть любое `falsy` значение и тогда результат выполнения будет отброшен либо объект с заранее известными полями, и тогда оверлей будет использовать их в своей работе.

Некоторые хуки являются информационными и могут использоваться для сайд-эффектов.

Выполнение хуков синхронное. В ряде случаев можно вернуть `{ preventDefault: true }` и сделать необходимые действия самостоятельно.

- [`onOverlayOpen`](#onoverlayopen)
- [`onOverlayClose`](#onoverlayclose)
- [`onOverlayContentShown`](#onoverlaycontentshown)
- [`onOverlayFallback`](#onoverlayfallback)
- [`onOverlayNavigate`](#onoverlaynavigate)
- [`onOverlayNewFrameOpened`](#onoverlaynewframeopened)
- [`onOverlayRelocate`](#onoverlayrelocate)
- [`onOverlayActiveDocumentChanged`](#onoverlayactivedocumentchanged)
- [`onOverlayPageChanged`](#onoverlaypagechanged)
- [`onOverlayHeaderHidden`](#onoverlayheaderhidden)
- [`onOverlayHeaderVisible`](#onoverlayheadervisible)
- [`onOverlayCloseButtonClick`](#onoverlayclosebuttonclick)
- [`onOverlayBackButtonClick`](#onoverlaybackbuttonclick)
- [`onOverlayPageChanged`](#onoverlaypagechanged)

### `onOverlayOpen`
```typescript
function onOverlayOpen(data: IBaseHookData): void;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

interface  IBaseHookData {
    /** урл или урлы, которые будут открыты */
    urls:  IOpenData[];
    /** корневой элемент оверлея */
    root:  HTMLElement;
    /** номер iframe в мультислайдере */
    index:  number;
    /** метаинформация для передачи в хуки */
    meta?: AnyJson;
}
```

Информационный хук, который вызывается прямо перед открытием оверлея. Может использоваться для скрытия скролла или отправки счетчиков.

```ts
window.Ya.turboOverlay.onOverlayOpen = ({ root }) => {
  console.log('overlay is opened');
  bodyScrollLock.disableBodyScroll(root)
}

// открывается с крестиком
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

/*
 * => 'overlay is open'
 * => лочится скролл страницы
 * => открывается оверлей
 */
```

### `onOverlayClose`
```typescript
function onOverlayClose(data: IBaseHookData): void;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

interface  IBaseHookData {
    /** урл или урлы, с которыми открывался оверлей */
    urls:  IOpenData[];
    /** корневой элемент оверлея */
    root:  HTMLElement;
    /** номер iframe в мультислайдере */
    index:  number;
    /** метаинформация для передачи в хуки */
    meta?: AnyJson;
}
```

Информационный хук, который вызывается прямо перед закрытием оверлея. Может использоваться, например, для восстановления скролла или отправки счетчиков.

```ts
window.Ya.turboOverlay.onOverlayClosed = ({ root }) => {
  console.log('overlay is closed');
  bodyScrollLock.enableBodyScroll(root)
}

// открывается с крестиком
window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/turbo?text=https://kp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

history.back()

/*
 * => 'overlay is closed'
 * => восстанавливается скролл страницы
 * => закрывается оверлей
 */
```

### `onOverlayContentShown`
### `onOverlayActiveDocumentChanged`
```typescript
function onOverlayContentShown(data: IShowHookData): IUpdateDisplayData;
function onOverlayActiveDocumentChanged(data: IShowHookData): IUpdateDisplayData;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

interface  IShowHookData {
    /** урл или урлы, с которыми открывался оверлей */
    urls:  IOpenData[];
    /** корневой элемент оверлея */
    root:  HTMLElement;
    /** номер iframe в мультислайдере */
    index:  number;
    /** метаинформация для передачи в хуки */
    meta?: AnyJson;
    /** тайтл страницы из post-message */
    title: string;
    /** урл страницы из post-message */
    displayUrl: string;
}

interface  IUpdateDisplayData {
    /** можно вернуть null, чтобы не менять или undefined, чтобы оставить текущее поведение */
    title?: string | null;
    /** можно вернуть null, чтобы не менять или undefined, чтобы оставить текущее поведение */
    displayUrl?: string | null;
}
```

`onOverlayContentShown` вызывается сразу после того как пришло событие о показе оверлея. Это означает, что какой-то контент загрузился и необходимо заменить урл и тайтл страницы (эти данные приходят из iframe).

Это происходит как при первичной загрузке оверлея, так и при навигации турбо-в-турбо, в т.ч. назад.

`onOverlayActiveDocumentChanged` означает, что пользователь доскролил до следующей статьи в бесконечной ленте.

С помощью этих хуков можно изменить урл, который окажется в адресной строке или тайтл, который увидит пользователь.

```ts
const onShow = ({ displayUrl, title }) => ({
  displayUrl: `/sidebar?q=${encodeURIComponent(displayUrl)}`,
  title: `[Турбо-страницы] ${title}`
});

window.Ya.turboOverlay.onOverlayContentShown = onShow;
window.Ya.turboOverlay.onOverlayActiveDocumentChanged = onShow;

window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/sidebar?q=%2Fturbo%3Ftext%3Dhttps%3A%2F%2Fkp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

/*
 * => открывается оверлей
 * => когда страница загружается, урл меняется на предоставленный (по сути тот же самый)
 * => к оригинальномоу тайтлу добавляется [Турбо-страницы]
 *
 * после клика по турбо-ссылке внутри оверлея
 * и загрузки новой страницы, show снова вызовется,
 * и урл заменится на соответствующий], а к
 * оригинальномай тайтлу добавится [Турбо-страницы]
 *
 * когда пользователь проскроллит до следующей статьи в
 * бесконечной ленте урл и тайтл так же изменятся на необходимый.
 */

// ----- более сложный пример:
window.Ya.turboOverlay.onOverlayContentShown = ({ displayUrl, title }) => {
    const text = new URL(location.href).searchParams.get('text');
    const url = new URL(text);

    if (text.pathname.indexOf('/pogoda') === 0) {
      return { displayUrl: `/sidebar?q=${encodeURIComponent(text)}` }
    }

    return { displayUrl: `/sidebar?q=${encodeURIComponent(displayUrl)}` }
};

window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https%3A%2F%2Fyandex.ru%2Fpogoda%3Flat%3D55.734085&lon=37.587013',
        displayUrl: '/sidebar_href=https%3A%2F%2Fyandex.ru%2Fpogoda%3Flat%3D55.734085%26lon%3D37.587013',
        originlUrl: 'https://kp.ru',
    }],
});

/*
 * В данном случае мы хотим сохранять
 * турбированный урл для всех страниц, кроме погоды,
 * которая проксирует на турбо со своего урла. Для погоды
 * мы хотим держать погодный урл.
 */
```


### `onOverlayFallback`
```typescript
function onOverlayFallback(data: IFallbackHookData): IPreventable;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

enum EFallbackTypes {
    /** пришло сообщение от оверлея */
    messageFallback =  'message',
    /** произошел fallback по таймауту */
    timeoutFallback =  'timeout',
    /** iframe выбросил ошибку */
    frameErrorFallback =  'frameError'
}

interface IFallbackHookData {
    /** урл или урлы, с которыми открывался оверлей */
    urls:  IOpenData[];
    /** корневой элемент оверлея */
    root:  HTMLElement;
    /** номер iframe в мультислайдере */
    index:  number;
    /** метаинформация для передачи в хуки */
    meta?: AnyJson;
    /** оригинальный урл, на который перезагрузится страница */
    originalUrl: string;
    /** тип фолбэка */
    fallbackType: EFallbackTypes;
    /** функция, выполняющая редирект */
    callback: (originalUrl: string): void;
}

interface  IPreventable {
    preventDefault?:  boolean;
}
```

Вызывается перед тем, как оверлей средиректит на оригинал. С помощью него можно отправить счетчики ошибки

```ts
window.Ya.turboOverlay.onOverlayFallback = ({ fallbackType }) => {
    switch (fallbackType) {
        case 'timeout':
            _sendCounter(['690.2719.2010.2922']); // /tech/turbo/fallback/timeout
            break;

        case 'frameError':
            _sendCounter(['690.2719.3513']); // /tech/turbo/frame-error;
            break;

        case 'message':
            _sendCounter(['690.2719.2010.3731']); // /tech/turbo/fallback/nodata
            break;
    }
};

window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/sidebar?q=%2Fturbo%3Ftext%3Dhttps%3A%2F%2Fkp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

/* Если произойдет фолбэк, функциия вызовется и отправятся счетчики */

// Иногда необходимо дождаться пока отправятся счетчики, в этом случае можно вернуть preventDefault
// и вызывать колбэк тогда, когда счетчики все-таки отправятся. Предположим, что функция sendCounter
// возвращает промис.

const sendFallbackCounter = (fallbackType) => {
    switch (fallbackType) {
        case 'timeout':
            return _sendCounter(['690.2719.2010.2922']); // /tech/turbo/fallback/timeout
        case 'frameError':
            return _sendCounter(['690.2719.3513']); // /tech/turbo/frame-error;
        case 'message':
            return _sendCounter(['690.2719.2010.3731']); // /tech/turbo/fallback/nodata
        default:
            return Promise.resolve();
    }
}

window.Ya.turboOverlay.onOverlayFallback = ({ fallbackType, callback, originalUrl }) => {
    sendFallbackCounter(fallbackType)
        .then(() => callback(originalUrl));

    return { preventDefault: true };
}

// в этом же примере при желании можно изменить originalUrl
```

### `onOverlayNavigate`
### `onOverlayRelocate`
### `onOverlayNewFrameOpened`
### `onOverlayPageChanged`
```typescript
function onOverlayNavigate(data: INavigateHookData): IUpdateDisplayUrl;
function onOverlayRelocate(data: INavigateHookData): IUpdateDisplayUrl;
function onOverlayNewFrameOpened(data: INavigateHookData): IUpdateDisplayUrl;
function onOverlayPageChanged(data: INavigateHookData): IUpdateDisplayUrl;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

interface INavigateHookData {
    /** урл или урлы, с которыми открывался оверлей */
    urls:  IOpenData[];
    /** корневой элемент оверлея */
    root:  HTMLElement;
    /** номер iframe в мультислайдере */
    index:  number;
    /** метаинформация для передачи в хуки */
    meta?: AnyJson;
    /** урл с которого произошла навигация */
    from: string;
    /** урл на который будет совершена навигация */
    to: string;
}

interface IUpdateDisplayUrl {
    /** можно вернуть null, чтобы не менять или undefined, чтобы оставить текущее поведение */
    displayUrl?: string | null;
}
```

Все четыре хука работают одинаковым образом, но вызываются для разных событий.
- `onOverlayNavigate` вызывается перед навигацией турбо-в-турбо. (`location.href = ...`)
- `onOverlayRelocate` вызывается перед навигацией турбо без записи в истории `location.replace(url)`
- `onOverlayNewFrameOpened` особая навигация, когда переход совершается не внутри текущего `iframe`,
    а рисуется новый iframe поверх текущего.
- `onOverlayPageChanged` вызывается при перелистывании страниц в мультислайдере.

Все хуки могут изменять дефолтный урл. Стоит заметить что для любых браузеров, кроме ios12 результат выполнения `onOverlayNavigate` будет отброшен. Это связано с тем, что вполть до загрузки страницы урл будет сохраняться (из-за нативной навигации)

Хуки можно использовать для замены урла на сервисный:

```ts
const navigate = ({ to }) => ({
    displayUrl: `/sidebar?q=${encodeURIComponent(to)}`,
});

window.Ya.turboOverlay = {
    ...window.Ya.turboOverlay,

    onOverlayNavigate: navigate,
    onOverlayRelocate: navigate,
    onOverlayNewFrameOpened: navigate,
    onOverlayPageChanged: navigate
}

window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/sidebar?q=%2Fturbo%3Ftext%3Dhttps%3A%2F%2Fkp.ru',
        originlUrl: 'https://kp.ru',
    }],
});
```

### `onOverlayHeaderHidden`
### `onoverlayHeaderVisible`
```typescript
function onOverlayHeaderHidden(data: INavigateHookData): void;
function onOverlayHeaderVisible(data: INavigateHookData): void;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

interface INavigateHookData {
    /** урл или урлы, с которыми открывался оверлей */
    urls:  IOpenData[];
    /** корневой элемент оверлея */
    root:  HTMLElement;
    /** номер iframe в мультислайдере */
    index:  number;
    /** метаинформация для передачи в хуки */
    meta?: AnyJson;
}
```

Информационные хуки, которые говорят, что оверлей спрятал или показал шапку (с кнопкой  назад).  Используется, например, внтури просмотрщика, чтобы имитировать фулскрин: https://jing.yandex-team.ru/files/werreour/20190902191937.mp4

Возвращаемый результат игнорируется.

```ts
window.Ya.turboOverlay.onOverlayHeaderHidden = () => {
    console.log('header hidden!');
};

window.Ya.turboOverlay.onOverlayHeaderVisible = () => {
    console.log('header visible!');
}

window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/sidebar?q=%2Fturbo%3Ftext%3Dhttps%3A%2F%2Fkp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

/*
 * => Открывается оверлей
 * Когда пользователь кликнет по изображению, спрячется шапка,
 * в консоль выведется 'header hidden'. После клика на крестик и
 * закрытия просмотрщика, шапка снова покажется
 */
```

### `onOverlayCloseButtonClick`
### `onOverlayBackButtonClick`
```typescript
function onOverlayCloseButtonClick(data: INavigateHookData): IPreventable;

type AnyJson = boolean | number | string | null | JsonArray | JsonMap;
interface JsonMap { [key:  string]: AnyJson; }
interface JsonArray extends Array<AnyJson> {}

interface IButtonHookData {
    /** урл или урлы, с которыми открывался оверлей */
    urls:  IOpenData[];
    /** корневой элемент оверлея */
    root:  HTMLElement;
    /** номер iframe в мультислайдере */
    index:  number;
    /** метаинформация для передачи в хуки */
    meta?: AnyJson;
    /** глубина оверлея (количество переходов турбо-в-турбо */
    depth: number;
}

interface  IPreventable {
    preventDefault?:  boolean;
}
```
В оба хука приходят данные о глубине турбо-страниц (сколько было переходов
турбо-в-турбо). Для первой страницы она будет 0, после первого перехода
турбо-в-турбо, он станет один и так далее.

В качестве результата могут вернуть `{ preventDefault: true }`. И тогда перехода назад не будет.

`onOverlayCloseButtonClick` вызывается по клику на крестик (справа в шапке). Внутри вызовет метод `close` оверлея, закрыв все переходы турбо-в-турбо.

`onOverlayBackButtonClick` на кнопку "назад" (слева в шапке). Внутри вызовет метод `window.history.back`, сделав один шаг назад по истории.

```ts
window.Ya.turboOverlay.onOverlayCloseButtonClick = ({ depth }) => {
    renderModal('Вы точно хотите закрыть турбо-страницы?').then(answer => {
        if (answer === 'ok') { window.Ya.turboOverlay.close() }
    })

    return { preventDefault: true };
};

// показываем крестик, чтобы пользователю было куда кликать.
window.Ya.turboOverlay.showCloseButton();

window.Ya.turboOverlay.open({
    urls: [{
        frameUrl: 'https://yandex.ru/turbo?text=https://kp.ru',
        displayUrl: '/sidebar?q=%2Fturbo%3Ftext%3Dhttps%3A%2F%2Fkp.ru',
        originlUrl: 'https://kp.ru',
    }],
});

/*
 * => Открывается оверлей, если пользователь кликнет по крестику,
 * то ему вначале придется согласиться с модалкой)
 */
```

### `onOverlayBrokenHistoryRecord`
`window.Ya.turboOverlay.` - оверлей наткнулся на  сломанную запись  в истории.

Оверлей очень сильно полагается на `history api`, которое, к сожалению, не всегда работает так как надо. На ios исторические записи могут теряться, плюс иногда мы ловим баги, что отдельные переходы в той же вкладке могут быть нетурбовыми
(без post-message). Не совсем ясно, что делать в таком случае и оверлей просто перезагружается в надежде,
что урл в адресной
строке правильный. Такое поведение можно предотвратить. Хук вызывается без параметров.

Сломанной считается запись с турбированной страницей, но без данных для воссоздания iframe.

Поведение можно остановить с помощью `preventDefault: true`. Оверлей закроется.

```ts
export interface IPreventable {
     preventDefault?: boolean;
}
```

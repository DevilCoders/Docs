## Тестирование попапов

Popup manager - это отдельный виджет и показ попапа может не заработать без его монтирования.

Чтобы смонтировать нужный виджет и popup manager, можно написать виджет обертку со слотами под нужные виджеты. Пример:

```js
export default Widget.describe({
    name: 'YaPlusOnboardingWithPopupManager',
    view: () => (
        <>
            <Slot name="yandexPlusOnboarding" />
            <Slot name="popupManager" />
        </>
    ),
    controller: ctx => ({
        slots: {
            yandexPlusOnboarding: YandexPlusOnboarding.create(ctx),
            popupManager: PopupManager.create(ctx),
        },
    }),
    directives: {static: true},
});
```

Далее задиспатчить нужный action, приводящий к открытию попапа, можно через SharedActionEmitter:

```js
const SharedActionEmitter = require('@yandex-market/apiary/client/sharedActionEmitter').default;

const globalSharedActionEmitter = new SharedActionEmitter();

...

const {showUserPopup} = require('@self/root/src/actions/popups');

globalSharedActionEmitter.dispatch(showUserPopup({id: 'yandexPlusOnboarding'}));
```

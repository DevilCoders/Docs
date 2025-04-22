# Виджет c кнопкой для чатов поддержки

Подробнее про использование виджета с кнопкой можно прочесть [здесь](./ui-button.md)
Использовать только для чатов находящихся в workspace `support`

[Storybook](https://messenger-test.s3.mds.yandex.net/storybook/widget/latest/index.html?path=/story/widget--ui-supportbutton)

```ts
import '@yandex-int/messenger.widget/lib/ui/supportbutton.css';
import {
    YandexSingleChatConfig,
    Widget,
    supportButtonUIFactory,
    yandexUnreadCounterFactory,
    presets,
} from '@yandex-int/messenger.widget';

const unreadCounterPlugin = yandexUnreadCounterFactory();

const ui = supportButtonUIFactory({
    unreadCounterPlugin,
});

const widget = new Widget(new YandexSingleChatConfig(
    presets.support(YOUR_SUPPORT_BOT_GUID),
    {
        serviceId: YOUR_SERVICE_ID,
    }
))
    .setPlugin(unreadCounterPlugin)
    .setUI(ui)
    .init();

ui.mount();
```

**supportButtonUIFactory**(props: [ButtonProps](./interfaces.md#buttonprops)): [SupportButtonUI](./interfaces.md#supportbuttonui)

`props`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`isMobile?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Мобильный вид виджета. Если не задан, вычисляется автоматически

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`autocloseable?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Если true, то при клике вне область попапа, попап будет закрываться

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`strategies?`: *Array\<[BehaviorStrategies](./interfaces.md#behaviorstrategies)>*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Стратегии открытия

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`badgeMaxCount?`: *number*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;При превышении указанного ограничения отобразится сокращенная форма записи значения счетчика (maxCount+)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`badgeType?`: *[BadgeType](./interfaces.md#badgetype)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Вид бейджика с количеством непрочитанных сообщений.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`collapsedDesktop?`: *[ButtonCollapsed](./interfaces.md#buttoncollapsed)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Состояние свёрнутости кнопки виджета в десктопном отображении.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`collapsedTouch?`: *[ButtonCollapsed](./interfaces.md#buttoncollapsed)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Состояние свёрнутости кнопки виджета в мобильном отображении.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`buttonText?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Текст кнопки виджета

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`unreadCounterPlugin?`: *[UnreadCounterPlugin](./interfaces.md#unreadcounterplugin)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Плагин кол-ва непрочитанных сообщений

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`paranjaVisible?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Если true паранжа будет видна
Для правильной работы необходимо монтировать кнопку в `body`
Паранжа не отключает скролл страницы, включать/отключать скролл можно в событие `onToggled`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`pageScrollController?`: *[PageScrollController](./interfaces.md#pagescrollcontroller)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Установить кастомный контроллер скролла страницы
Нужен для управления поведением скролла страницы при открытии попапа
Контроллер по умолчанию - отключает скролл страницы в мобильном режиме

# Виджет попап для чатов с поддержкой

Подробнее про использование виджета попап можно прочесть [здесь](./ui-popup.md)
Использовать только для чатов находящихся в workspace `support`

[Storybook](https://messenger-test.s3.mds.yandex.net/storybook/widget/latest/index.html?path=/story/widget--ui-supportpopup)

## Пример интеграции виджета поддержки попапом

```ts
import '@yandex-int/messenger.widget/lib/ui/supportpopup.css';
import {
    YandexSingleChatConfig,
    Widget,
    supportPopupUIFactory,
    yandexUnreadCounterFactory,
    presets,
} from '@yandex-int/messenger.widget';

const unreadCounterPlugin = yandexUnreadCounterFactory();

const ui = supportPopupUIFactory({
    unreadCounterPlugin,
});

const widget = new Widget(new YandexSingleChatConfig(
    presets.support(YOUR_SUPPORT_BOT_GUID),
    {
        serviceId: YOUR_SERVICE_ID,
    }
))
    .setPlugin(unreadCounterPlugin)
    .setUI(ui)
    .init();

ui.mount();
```

**supportPopupUIFactory**(props: [SupportPopupProps](./interfaces.md#supportpopupprops)): [Popup](./interfaces.md#popup)\<[ButtonProps](./interfaces.md#buttonprops), [Props](./interfaces.md#props)>

`props`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`unreadCounterPlugin?`: *[UnreadCounterPlugin](./interfaces.md#unreadcounterplugin)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Плагин кол-ва непрочитанных сообщений

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`isMobile?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Мобильный вид виджета. Если не задан, вычисляется автоматически

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`popupTargetNode?`: *HTMLElement*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Элемент от которого позиционируется попап

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`popupTargetPosition?`: *[TargetPosition](./interfaces.md#targetposition)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Используется вместе с popupTargetNode для позиции появления попапа от элемента.
Default bottom-left

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`paranjaVisible?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Если true паранжа будет видна
Паранжа не отключает скролл страницы, включать/отключать скролл можно в событие `onToggled`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`calculatePosition?`: *(el: HTMLElement, anchor: HTMLElement, targetPosition: [TargetPosition](./interfaces.md#targetposition), prevPosition: [Place](./interfaces.md#place)): [Place](./interfaces.md#place)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Пользовательская функция расчета позиции попапа

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`autocloseable?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Если true, то при клике вне область попапа, попап будет закрываться

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`strategies?`: *Array\<[BehaviorStrategies](./interfaces.md#behaviorstrategies)>*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Стратегии открытия

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`pageScrollController?`: *[PageScrollController](./interfaces.md#pagescrollcontroller)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Установить кастомный контроллер скролла страницы
Нужен для управления поведением скролла страницы при открытии попапа
Контроллер по умолчанию - отключает скролл страницы в мобильном режиме
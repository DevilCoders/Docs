# Popup ui

Интерфейс виджета для открытия мессенджера в popup-е.
Подходит, например, если у вас есть своя кнопка открытия виджета.

Если задан параметр `popupTargetNode` попап будет спозиционирован относительно заданного узла
(настроить позиционирования можно через `popupTargetPosition`), иначе попап откроется
в правом нижнем углу.

Параметры `popupTargetNode` и `popupTargetPosition` не обязательно задавать сразу,
в любой момент после инициализации виджета, можно вызвать метод `Popup::setPopupTarget`

Для того что бы программно открыть виджет необходимо использовать `Widget::show`

[Storybook](https://messenger-test.s3.mds.yandex.net/storybook/widget/latest/index.html?path=/story/widget--ui-popup)

```ts
import '@yandex-int/messenger.widget/lib/ui/popup.css';
import {
    YandexConfig,
    Widget,
    popupUIFactory,
} from '@yandex-int/messenger.widget';

const ui = popupUIFactory({
    popupTargetNode: document.getElementById('my_custom_chat_button'),
});

const widget = new Widget(new YandexConfig({
    serviceId: YOUR_SERVICE_ID,
    iframeOpenData: {
        // Параметры открытия виджета (идентификатор чата, идентификатор бота и т.п.)
        // [подробнее](./interfaces.md#baseiframeopenparams)
    },
}))
    .setUI(ui)
    .init();

ui.mount();

document.getElementById('button').addEventListener('click', () => {
    widget.show();
});
```

В случае если нужно отображение кол-ва непрочитанных сообщений можно подключить плагин UnreadCounter

```ts
import '@yandex-int/messenger.widget/lib/ui/popup.css';
import {
    YandexConfig,
    Widget,
    popupUIFactory,
    yandexUnreadCountFactory,
} from '@yandex-int/messenger.widget';

const ui = new popupUIFactory({});
const unreadCounter = yandexUnreadCountFactory();

unreadCounter.onChanged.addListener(({ data }) => console.log(data));

const widget = new Widget(new YandexConfig({
    serviceId: -1,
    iframeOpenData: {
        // Параметры открытия виджета (идентификатор чата, идентификатор бота и т.п.)
        // [подробнее](./interfaces.md#baseiframeopenparams)
    },
}))
    .addPlugin(unreadCounter)
    .setUI(ui);
    .init();

ui.mount();
```

**popupUIFactory**(props: [PopupProps](./interfaces.md#popupprops)): [Popup](./interfaces.md#popup)\<[PopupProps](./interfaces.md#popupprops), [Props](./interfaces.md#props)>

`props`

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

---

Смонтировать UI в указанный DOM узел.

**mount**(): void

---

Установка/удаления элемента, откносительно которого будет открыт попап

**setPopupTarget**(target: HTMLElement, position?: [TargetPosition](./interfaces.md#targetposition)): void

`target`: HTMLElement

Элемент, относительно которого будет открыт попап.
Если undefined то попап начнет открываться сбоку.

`position`: [TargetPosition](./interfaces.md#targetposition)

Позиция попапа

---

`hidden`: *boolean*

>

Скрыт ли попап

`onToggled`: *[Event](./interfaces.md#event)\<[OnToggledEvent](./interfaces.md#ontoggledevent)>*

>

Вызывается при открытии/закрытии попапа

---

# CSS переменные

`--yandex-mssngr-widget-bg-color`: `#fff`

>Цвет фона

---

`--yandex-mssngr-widget-text-color`: `#292c33`

>Цвeт текста

---

`--yandex-mssngr-widget-error-button-color`: `#1c70c4`

>Цвет текста кнопки повторить

---

`--yandex-mssngr-widget-loader-spinner-color`: `#00a8a8`

>Цвет спинера

---

`--yandex-mssngr-widget-fullscreen-left`: `0`

>Левый отступ в полноэкранном режиме

---

`--yandex-mssngr-widget-fullscreen-right`: `0`

>Правй отступ в полноэкранном режиме

---

`--yandex-mssngr-widget-fullscreen-top`: `0`

>Верхний отступ в полноэкранном режиме

---

`--yandex-mssngr-widget-fullscreen-bottom`: `0`

>Нижний отступ координата в полноэкранном режиме

---

`--yandex-mssngr-widget-fullscreen-z-index`: `10050`

>z-index полноэкранного режима

---

`--yandex-mssngr-widget-popup-base-z-index`: `10000`

>Базовый z-index попапа.
    Сам попап находится на +10
    Паранжа на +5

---

`--yandex-mssngr-widget-popup-mobile-header-height`: `40px`

>Высота мобильной шапки

---

`--yandex-mssngr-widget-popup-width`: `360px`

>Ширина попапа

---

`--yandex-mssngr-widget-popup-height`: `640px`

>Высота попапа

---

`--yandex-mssngr-widget-popup-transition-time`: `.4s`

>Время отображения попапа

---

`--yandex-mssngr-widget-popup-timing-func`: `ease`

>Ease функция отображения попапа

---

`--yandex-mssngr-widget-popup-paranja-color`: `rgba(0, 0, 0, .56)`

>Цвет паранжи

---

`--yandex-mssngr-widget-popup-ui-fixed-offset-bottom`: `20px`

>Отступ от попапа снизу

---

`--yandex-mssngr-widget-popup-ui-fixed-offset-right`: `20px`

>Отступ от попапа справа

---

`--yandex-mssngr-widget-popup-ui-border-radius`: `4px`

>Радиус углов попапа

---
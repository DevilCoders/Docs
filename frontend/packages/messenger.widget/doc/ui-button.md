# Button ui

Классический виджет с кнопкой. Кнопка отображается в правом нижнем углу

[Storybook](https://messenger-test.s3.mds.yandex.net/storybook/widget/latest/index.html?path=/story/widget--ui-button)

```ts
import '@yandex-int/messenger.widget/lib/ui/button.css';
import {
    YandexConfig,
    Widget,
    buttonUIFactory,
    yandexUnreadCounterFactory,
} from '@yandex-int/messenger.widget';

const unreadCounterPlugin = yandexUnreadCounterFactory();

const ui = buttonUIFactory({
   unreadCounterPlugin,
});

const widget = new Widget(new YandexConfig({
    serviceId: YOUR_SERVICE_ID,
    iframeOpenData: {
        // Параметры открытия виджета (идентификатор чата, идентификатор бота и т.п.)
        // [подробнее](./interfaces.md#baseiframeopenparams)
    },
}))
    .setPlugin(unreadCounterPlugin)
    .setUI(ui)
    .init();

ui.mount();
```

**buttonUIFactory**(props: [ButtonProps](./interfaces.md#buttonprops)): [ButtonUI](./interfaces.md#buttonui)

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

`--yandex-mssngr-widget-badge-bg-color`: `red`

>Цвет фона баджа

---

`--yandex-mssngr-widget-badge-text-color`: `#fff`

>Цвет текста в бадже

---

`--yandex-mssngr-widget-button-large-scale`: `1.5`

>Масштаб увеличенной иконки

---

`--yandex-mssngr-widget-button-size`: `40px`

>Размер кнопки

---

`--yandex-mssngr-widget-button-max-width`: `280px`

>Максимальная ширина кнопки

---

`--yandex-mssngr-widget-button-border-radius`: `13px`

>Радиус кнопки

---

`--yandex-mssngr-widget-button-clickable-area-extra-space`: `20px`

>Размер активной области вокруг кнопки

---

`--yandex-mssngr-widget-button-icon-size`: `28px`

>Размер иконки мессенджера

---

`--yandex-mssngr-widget-button-ui-static-offset-right`: `20px`

>Правый отступ кнопки

---

`--yandex-mssngr-widget-button-ui-static-offset-bottom`: `20px`

>Нижний отступ кнопки

---

`--yandex-mssngr-widget-button-ui-z-index`: `var(--popup-base-z-index)`

>z-index кнопки

---

`--yandex-mssngr-widget-button-ui-popup-border-radius`: `13px`

>Радиус углов попапа

---
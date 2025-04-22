# Block ui

Интерфейс виджета для инлайн встраивания в страницу.
Подходит, например, для трансляций (когда чат находится рядом с видео).

Виджет будет занимать 100% высоты и ширины узла в который он встроен

[Storybook](https://messenger-test.s3.mds.yandex.net/storybook/widget/latest/index.html?path=/story/widget--ui-block)

## Получение кол-ва непрочитанных сообщений в чате
В случае если вы планируете постоянно отображать виджет - можно использовать событие
виджета `counter` ([подробнее о том как подписываться на события](./events.md)).
Иначе можно подключить плагин [UnreadCounter](./plugin-unread-counter.md).

```ts
import '@yandex-int/messenger.widget/lib/ui/button.css';
import {
    YandexSingleBlockChatConfig,
    blockUIfactory,
    Widget,
} from '@yandex-int/messenger.widget';

const ui = new Block();
const widget = new Widget(new YandexSingleBlockChatConfig(
    {
        serviceId: YOUR_SERVICE_ID,
        iframeOpenData: {
            // Параметры открытия виджета (идентификатор чата, идентификатор бота и т.п.)
            // [подробнее](./interfaces.md#baseiframeopenparams)
        },
    },
))
  .setUI(ui)
  .init();

ui.mount(document.getElementById('widget_wrapper_node'))

widget.show();
```

**blockUIFactory**(): [Block](./interfaces.md#block)

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
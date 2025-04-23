# Подключение виджета в React приложение

## Пример подключения виджета попапа с кастомной кнопкой и счетчиком непрочитанных
В этом примере описан вариант с доступом к виджету из любой точки приложения. Если вам не требуется доступ к API виджета, виджет можно инициализировать непосредственно в компоненте.

{% note alert %}
Виджет не поддерживает `SSR`. В случае если ваше приложение использует `SSR` не вызывайте `Widget::init` в время серверного рендринга.

`Widget::init` должен быть вызван сразу после конфигурации виджета. В противном случае любое обращение к его API или API UI плагина приведет к ошибке.
{% endnote %}

```ts
// widget.ts
import '@yandex-int/messenger.widget/lib/ui/popup.css';
import {
    YandexConfig,
    Widget,
    popupUIFactory,
    yandexUnreadCounterFactory,
} from '@yandex-int/messenger.widget';

export const unreadCounter = yandexUnreadCounterFactory();

export const ui = popupUIFactory({});

export const widget = new Widget(new YandexConfig({
    serviceId: YOUR_SERVICE_ID,
}))
    .addPlugin(unreadCounter)
    .setUI(ui);

// Инициализация виджета требует доступ к window,
// так же вызов widget.init можно перенести в хук
if (NOT_SSR) {
    widget.init();
}

```

```tsx
// WidgetContext.ts
import React from 'react';
import { ui, widget, unreadCounter } from './widget.ts';

const widgetContextValue = {
    ui,
    widget,
    unreadCounter,
};

export const WidgetContext = React.createContext(widgetContextValue);

export const useWidgetContext() {
    return React.useContext(WidgetContext);
}

export const WidgetContextProvider: React.FC = ({ children }) => {
    return (
        <WidgetContext.Provider value={widgetContextValue}>
            {children}
        </WidgetContext.Provider>
    );
}

```

```tsx
// WidgetMount.ts
import React from 'react';
import { useWidgetContext } from './WidgetContext.ts';

export const WidgetMount: React.FC = () => {
    const { ui } = useWidgetContext();

    React.useEffect(() => {
        ui.mount();
    }, []);

    return null;
}

```

```tsx
// MyWidgetButton.ts
import React from 'react';
import { useWidgetContext } from './WidgetContext.ts';

export const MyWidgetButton: React.FC = () => {
    const buttonRef = React.useRef(null);
    const [unread, setUnread] = React.useState(0);
    const { ui, widget, unreadCounter } = useWidgetContext();

    const handleClick = React.useCallback(() => {
        widget.show();
    }, [widget]);

    React.useEffect(() => {
        if (buttonRef.current) {
            ui.c(target: buttonRef.current);
        }
    }, [ui]);

    React.useEffect(() => {
        function handler(data) {
            setUnread(data.value || 0);
        }

        unreadCounter.onChanged.addListener(handler);

        return () => {
            unreadCounter.onChanged.removeListener(handler);
        }
    }, []);

    return (
        <button onClick={handleClick} ref={buttonRef}>
            Мессенджер {unread}
        </button>
    ); 
}
```

```tsx
// App.tsx
import React from 'react';
import { WidgetContextProvider } from './WidgetContext.ts';
import { WidgetMount } from './WidgetMount.ts';
import { MyWidgetButton } from './MyWidgetButton.ts';

export const App: React.FC = () => {
    return (
        <WidgetContextProvider>
            <WidgetMount />
            <MyWidgetButton />
        </WidgetContextProvider>
    );
}

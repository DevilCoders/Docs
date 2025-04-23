# @yandex/tap-components 🚀

Набор общих React компонентов для tap-сервисов. 
Документация и примеры доступны в [Storybook](https://tap.s3.yandex.net/tap-components-storybook/v0.4.0/index.html?path=/docs/tap-components-documentation--readme).

## Установка

```bash
#⠀Пакет с компонентами
npm install --save git+ssh://github.com/yandex/tap-components#v0.4.0

#⠀Peer зависимости
npm install --save react@16 react-dom@16 react-router@5
```

## Использование

Пример использования компонента:

```typescript jsx
import React from 'react';
import { AdaptiveGrid, AdaptiveGridItem } from '@yandex/tap-components/AdaptiveGrid';

const Component: React.FC = () => {
    return  (
        <AdaptiveGrid>
           <div>Item 1</div>
           <div>Item 2</div>
           <AdaptiveGridItem fullWidth>Banner</AdaptiveGridItem>
           <div>Item 3</div>
           <div>Item 4</div>
        </AdaptiveGrid>
    );
};
```

Пример использования хука:

```typescript jsx
import React, { useRef } from 'react';
import { useVisible } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const ref = useRef();
    const isVisible = useVisible(ref);

    return <div ref={ref} />;
}
```

Пример использования хелпера:

```typescript jsx
import React from 'react';
import { isIOS } from '@yandex-int/tap-components/helpers';

const Component: React.FC = () => {
    return <div>{isIOS() ? 'A' : 'B'}</div>;
}
```

## Поддерживаемые браузеры

Компоненты разрабатываются под мобильные платформы Яндекса:
- Приложение «Яндекс»
- Мобильный Яндекс.Браузер

На Android tap-сервисы запускаются в Яндекс.Браузере, поэтому работа компонентов не зависит от версии ОС.
На iOS tap-сервисы запускается в WKWebView, который похож на iOS Safari и зависит от версии iOS.

| Browser           | Поддерживаемая версия |
| ----------------- | --------------------- |
| Yandex Browser    | >= 20.0               |
| iOS Safari        | >= 13.0               |

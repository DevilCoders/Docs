# @yandex-int/tap-components 🚀 ![package version](https://badger.yandex-team.ru/npm/@yandex-int/tap-components/version.svg)

Набор общих React компонентов для tap-сервисов. 
Документация и примеры доступны в [Storybook](https://lego-docs.s3.mds.yandex.net/story/dev/index.html?path=/story/tap-components-documentation--readme).

> ⚠️ Исходный код пакета автоматически [публикуется на github.com](https://github.com/yandex/tap-components).

Если у вас возникли проблемы или вопросы, то можно:

- Создавать тикет в [startrek](https://st.yandex-team.ru/TAP) (очередь `TAP`).

## Установка

```bash
#⠀пакет с компонентами
npm i -P @yandex-int/tap-components --registry http://npm.yandex-team.ru
#⠀peer зависимости
npm i -P react react-dom react-router
```

## Использование

Пример использования компонента:

```typescript jsx
import React from 'react';
import { AdaptiveGrid, AdaptiveGridItem } from '@yandex-int/tap-components/AdaptiveGrid';

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

| Browser        | Поддерживаемая версия |
| -------------- | --------------------- |
| Yandex Browser | `>=` 17.0             |
| iOS Safari     | `>=` 10.0             |
| ChromeAndroid  | `>=` 51.0             |
| Samsung        | `>=` 9.0              |
| OperaMobile    | `>=` 60.0             |
| Chrome         | `>=` 72.0             |
| Firefox        | `>=` 78.0             |
| Edge           | `>=` 85.0             |
| Safari         | `>=` 10.0             |
| Opera          | `>=` 71.0             |

Особенности работы в турбоаппах:

- На iOS tap-сервисы запускается в WKWebView, который похож на iOS Safari и зависит от версии iOS.

> ⚠️ **Рекомендуется также обращать внимание на раздел "Поддержка" в документации отдельных компонентов, для работы некоторых компонентов в браузерах из списка выше необходимы полифиллы:**
* [`IntersectionObserver`](https://github.com/w3c/IntersectionObserver/tree/master/polyfill)

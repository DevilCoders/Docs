# SideBlock

Модальное окно (шторка), которое при открытии появляется в нижней части экрана и не скрывает полностью открытый в данный момент интерфейс.

Возможности:

- проскролливание дочерних элементов вверх/вниз;
- закрытие свайпом вниз;
- закрытие по тапу вне контента окна.

Если внутри шторки есть скроллящиеся элементы, необходимо использовать хук `useSideBlockLock` или
вспомогательный компонент `SideBlockLock`, чтобы предотвратить свайп во время скролла.

## Пример использования

### Использование компонента без скролла

```typescript jsx
import React, { useState,useCallback } from 'react';
import { SideBlock } from '@yandex-int/tap-components/SideBlock';

const onError = error => console.error(error.message);

const App: React.FC = () => {
    const [isVisible, setVisible] = useState(true);

    const onClose = useCallback(() => { setVisible(false) }, []);

    return (
        <SideBlock
            zIndex={400}
            visible={isVisible}
            onClose={onClose}
            onError={onError}
        >
            <div style={{ padding: '16px', backgroundColor: '#fff' }}>
                <h2>Обратите внимание</h2>
                <div>Важная информация</div>
            </div>
        </SideBlock>
    );
};
```

### Использование компонента со скроллом

```typescript jsx
import React, { useState, useCallback, useRef } from 'react';
import { SideBlock, useSideBlockLock } from '@yandex-int/tap-components/SideBlock';
import { VerticalScroll } from '@yandex-int/tap-components/VerticalScroll';

const Scroll: React.FC = ({ children }) => {
    const scrollRef = useRef<HTMLDivElement | null>(null);

    // Блокирует свайп модалки в момент скролла контента
    useSideBlockLock({ targetRef: scrollRef });

    return (
        <VerticalScroll ref={scrollRef} style={{ maxHeight: '150px' }}>
            {children}
        </VerticalScroll>
    );
};

const App: React.FC = () => {
    const [isVisible, setVisible] = useState(true);

    const onClose = useCallback(() => { setVisible(false) }, []);

    return (
        <SideBlock
            zIndex={400}
            visible={isVisible}
            onClose={onClose}
        >
            <Scroll>
                ...
                Длинный контент
                ...
            </Scroll>
        </SideBlock>
    );
};
```

## Примеры

{{%story:::tap-components-components-sideblock--playground%}}

## Свойства

| Свойство           | Тип                                    | Описание                                                                                                  |
| ------------------ | -------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| allowSwipe?        | `boolean`                              | Указывает на возможность смахнуть шторку свайпом. По умолчанию `true`                                     |
| allowOutsideClick? | `boolean`                              | Указывает на возможность закрыть шторку нажатием снаружи. Также активируется при `allowSwipe: true`       |
| children           | `React.ReactNode`                      | Содержимое шторки                                                                                         |
| className?         | `string`                               | Дополнительный класс у корневого DOM-элемента                                                             |
| contentClassName?  | `string`                               | Класс контейнера, в котором рисуется содержимое                                                           |
| onClose?           | `() => void`                           | Обработчик закрытия шторки                                                                                |
| onError?           | `ErrorHandler`                         | Функция, которая вызывается, если произошла ошибка при попытке заблокировать взаимодействие с приложением |
| onTransitionEnd?   | `(isSideBlockOpened: boolean) => void` | Функция, которая вызывается в момент окончания анимации открытия / закрытия шторки                        |
| rootElement?       | `Element | null`                       | Корневой элемент, в котором создается модальное окно. По умолчанию `document.body`                        |
| visible            | `boolean`                              | Флаг, указывающий состояние шторки: открыта / закрыта                                                     |
| zIndex?            | `number`                               | `z-index` контейнера                                                                                      |


```typescript jsx
type ErrorHandler = (err: Error) => void;
```

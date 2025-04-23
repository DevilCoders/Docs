# ContextMenuModal

Модальное окно с контекстным меню.

## Пример использования

```typescript jsx
import React, { useCallback, useState } from 'react';
import { compose } from '@bem-react/core';
import { ContextMenuModal } from '@yandex-int/tap-components/ContextMenuModal';
import { ListItem } from '@yandex-int/tap-components/List';
import { Text as TextBase, withWeightBold } from '@yandex-lego/components/Text';

const Text = compose(withWeightBold)(TextBase);

const App: React.FC = () => {
    const [isVisible, setIsVisible] = useState(true);

    const onClose = useCallback(() => setIsVisible(false), [setIsVisible]);

    return (
        <ContextMenuModal
            visible={isVisible}
            onClose={onClose}
            title={(
                <Text
                    as="h2"
                    typography="headline-m"
                    weight="bold"
                >
                    Действия
                </Text>
            )}
        >
            <ListItem onClick={() => console.log('Change count clicked!')}>
                Изменить количество
            </ListItem>
            <ListItem onClick={() => console.log('Remove clicked!')}>
                Удалить из корзины
            </ListItem>
        </ContextMenuModal>
    );
};
```

## Пример

{{%story:::tap-components-components-contextmenumodal--playground%}}

## Свойства

| Свойство   | Тип               | Описание                                            |
| ---------- | ----------------- | --------------------------------------------------- |
| children?  | `React.ReactNode` | Список пунктов меню, реализованных через `ListItem` |
| className? | `string`          | Дополнительный класс у корневого DOM-элемента       |
| onClose?   | `() => void`      | Обработчик закрытия модального окна                 |
| title?     | `React.ReactNode` | Заголовок модального окна                           |
| visible    | `boolean`         | Видно ли модальное окно                             |

Также поддерживаются все остальные свойства компонента [SideBlock](/?path=/docs/tap-components-components-sideblock--playground)

## CSS переменные

| Переменная                        | Тип     | Описание                          |
| --------------------------------- | ------- | --------------------------------- |
| --context-menu-modal-text-color   | `color` | Цвет текста модального меню       |
| --context-menu-modal-bg-color     | `color` | Цвет фона модального меню         |
| --context-menu-modal-side-padding | `px`    | Отступ внутри окна слева и справа |

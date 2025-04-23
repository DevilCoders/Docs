# CountSelectModal

Модальное окно выбора количества.

## Пример использования

```typescript jsx
import React, { useCallback, useState } from 'react';
import { compose } from '@bem-react/core';

import { Button as ButtonBase, withSizeM, withViewAction, withWidthMax } from '@yandex-int/tap-components/Button';
import { CountSelect } from '@yandex-int/tap-components/CountSelect';
import { CountSelectModal } from '@yandex-int/tap-components/CountSelectModal';

const Button = compose(withSizeM, withViewAction, withWidthMax)(ButtonBase);

const App: React.FC = () => {
    const [isVisible, setIsVisible] = useState(true);
    const [count, setCount] = useState(1);

    const onClose = useCallback(() => setIsVisible(false), [setIsVisible]);
    const onButtonClick = useCallback(() => {
        console.log(`Selected ${count}!`);
        onClose();
    });

    return (
        <CountSelectModal
            visible={isVisible}
            title="Количество"
            countSelect={<CountSelect count={count} onChange={setCount} />}
            controls={<Button size="m" view="action" width="max" onClick={onButtonClick}>Выбрать</Button>}
            onClose={onClose}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-countselectmodal--playground%}}

## Свойства

| Свойство    | Тип               | Описание                                       | Рекомендуемые компоненты |
| ----------- | ----------------- | ---------------------------------------------- | ------------------------ |
| className?  | `string`          | Дополнительный класс у корневого DOM-элемента  |                          |
| controls?   | `React.ReactNode` | Блок контролов, например, подтверждения выбора | `Button`                 |
| countSelect | `React.ReactNode` | Блок контрола выбора количества                | `CountSelect`            |
| onClose?    | `() => void`      | Обработчик закрытия окна выбора количества     |                          |
| title?      | `React.ReactNode` | Заголовок модального окна                      | `string`, `Text`         |
| visible     | `boolean`         | Видно ли модальное окно                        |                          |

Также поддерживаются все остальные свойства компонента [SideBlock](/?path=/docs/tap-components-components-sideblock--playground)

## CSS переменные

| Переменная                        | Тип     | Описание                          |
| --------------------------------- | ------- | --------------------------------- |
| --count-select-modal-text-color   | `color` | Цвет текста модального меню       |
| --count-select-modal-bg-color     | `color` | Цвет фона модального меню         |
| --count-select-modal-side-padding | `px`    | Отступ внутри окна слева и справа |


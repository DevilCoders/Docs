# useBackButton

Позволяет подписаться на нажатие системной кнопки «Back» на Android, а также кнопки «Назад» в браузере.

Компонент работает через History API. В момент активации хука создается запись в истории, которая отслеживается через событие `popstate`. Если запись пропала из истории, то вызывается `callback`, и запись снова добавляется в историю.

**Важно!** В один момент времени только один инстанс `useBackButton` отслеживает кнопку Back. Записи в историю браузера добавляются в порядке активации хуков, поэтому срабатывает только самый последний обработчик в хронологическом порядке.

Возможности:

- Вызов функции при попытке навигации назад по истории браузера.
- Блокировка навигации назад по истории браузера.
- Поддержка неограниченного количества `useBackButton` (активен только самый последний).
- Частичная поддержка совместной работы с `StackNavigator` (только при использовании `BrowserRouter`).

## Пример использования

### Минимальный пример

```typescript jsx
import React from 'react';
import { useBackButton } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    // Компонент заблокирует навигацию назад по истории браузера
    useBackButton(() => {
        console.log('Back button pressed!');
    });

    return null;
};
```

### Модальное окно

```typescript jsx
import React, { useState } from 'react';
import { useBackButton } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const [isVisible, setVisible] = useState(false);

    useBackButton(() => {
        // Закрываем модалку при нажатии на кнопку Back
        setVisible(false);
    }, {
        // Не следим за кнопкой Back, когда модалку не видно
        enabled: isVisible
    });

    return (
        <>
            <button onClick={() => setVisible(true)}>Show Modal</button>
            <Modal isVisible={isVisible} />
        </>
    );
};
```

## Примеры

### Модальные окна

{{%story:::tap-components-hooks-usebackbutton--modals%}}

### Пошаговая форма

{{%story:::tap-components-hooks-usebackbutton--steps%}}

## Параметры

```typescript jsx
function useBackButton(callback: () => void, options: { enabled?: boolean }): void;
```

| Свойство         | Тип          | Описание                                               |
| ---------------- | ------------ | ------------------------------------------------------ |
| callback         | `() => void` | Функция, которая вызывается при нажатии кнопки Back    |
| options?         | `object`     | Параметры хука                                         |
| options.enabled? | `boolean`    | Включает отслеживание кнопки Back. По умолчанию `true` |

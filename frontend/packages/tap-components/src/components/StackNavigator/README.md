# StackNavigator

Компонент для навигации между экранами. При переходах между url сохраняется предыдущий экран в DOM дереве, чтобы:

- Сохранять позицию скроллов внутри экрана (как самого экрана, так и элементов внутри, например, каруселей).
- Сохранять стейт элементов внутри экрана (например, значения полей в формах).
- Быстро показывать предыдущий экран при навигации назад за счет того, что экран уже отрисован.

Компонент зависит от библиотеки `react-router`. Для корректной работы компонента необходимо обернуть навигатор в компонент роутера.

Ограничения:

- Не поддерживается навигация через кнопку «Вперед», так как этой кнопки нет в SuperApp.
- Экраны не могут использовать параметры роутера напрямую (через хук `useParams()`), так как в один момент времени может быть отрисовано несколько одинаковых экранов с разными параметрами. Правильные параметры экрана приходят внутри props экрана.
- Поддерживается только fullscreen

## Пример использования

```typescript jsx
import React, { memo, useCallback } from 'react';
import { BrowserRouter, Link } from 'react-router-dom';
import { createStackNavigator, useNavigation } from '@yandex-int/tap-components/StackNavigator';

const Navigator = createStackNavigator(
    [
        {
            path: '/',
            exact: true,
            component: memo(() => <MainScreen />),
        },
        {
            path: '/details/:id',
            exact: true,
            component: memo(({ params: { id } }) => <DetailsScreen id={id} />),
        },
    ],
    {
        // Рендерим в DOM максимум 10 экранов
        maxDepth: 10,
        // iOS-like анимация переходов между экранами
        transitions: true,
    },
);

const MainScreen: React.FC = () => {
    return (
        <>
            <div>MainScreen</div>
            <Link to="/details/id-123">Go to details</Link>
        </>
    );
};

const DetailsScreen: React.FC<{ id: string }> = props => {
    const navigation = useNavigation();

    const onBackwardClick = useCallback(() => {
        navigation.back();
    }, [navigation]);

    return (
        <>
            <div>DetailsScreen for {props.id}</div>
            <button onClick={onBackwardClick}>Go back</button>
        </>
    );
};

const App: React.FC = () => {
    return (
        <BrowserRouter>
            <Navigator />
        </BrowserRouter>
    );
};
```

## Пример

{{%story:::tap-components-components-stacknavigator--playground%}}

## Хуки

### useNavigation

```typescript jsx
import { useNavigation } from '@yandex-int/tap-components/StackNavigator';

const navigation = useNavigation();

// Возврат на предыдущий экран
navigation.back();

// Возврат на конкретный экран в стеке (будет взят самый верхний, если их несколько)
// Если экран отсутствует в стеке, то будет заменён текущий
navigation.backToScreen({ url: '/' });
```

### useScreenVisible

```typescript jsx
import { useScreenVisible } from '@yandex-int/tap-components/StackNavigator';

// В стеке может быть множество экранов. Этот хук позволяет узнать, виден ли текущий экран пользователю
const isScreenVisible = useScreenVisible();
```

### useScreenRef

```typescript jsx
import { useScreenRef } from '@yandex-int/tap-components/StackNavigator';

// Возвращает `ref` на текущий экран
const screenRef = useScreenRef();
```

### useTransition

```typescript jsx
import { useTransition } from '@yandex-int/tap-components/StackNavigator';

// Хук позволяет узнать, анимируется ли текущий экран
const isTransition = useTransition();
```

## CSS-переменные

| Переменная                                | Тип     | Описание         |
| ----------------------------------------- | ------- | ---------------- |
| --stack-navigator-screen-background-color | `color` | Цвет фона экрана |

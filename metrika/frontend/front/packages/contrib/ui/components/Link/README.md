# Метрика Ссылки

## `Link`

React-router ссылка.

## `ExternalLink`

Внешняя ссылка.

### `saveParams`

URL параметры, которые стоит сохранить при переходе:

```jsx
<Link to="/list" saveParams={['param1', 'param2']}>Home</Link>;
```

В примере выше, если текущий `window.location.href` будет `https://metrika.ru?param1=123&param2=abcd&param3=thri`,
то ссылка будет вести на `https://metrika.ru?param1=123&param2=abcd`. То есть сохранились параметры `param1` и `param2`,
а все остальное выбросилось.

### `clear`

Сбрасывает тему и стили Лего ссылки:

```jsx
<Link clear to="/list">Home</Link>;
```

### Остальные props

Остальные props такие же как и у компонента `Link` из `@yandex-lego/components`. Например, вот ссылка с темой `black`:

```jsx
<Link to="/internal/list" theme="black">List</Link>
```

А вот это псевдо-ссылка, с соответствующей темой и обработчиком:

```jsx
<Link
    pseudo
    theme="pseudo"
    onClick={() => {
        console.log('Hi!');
    }}
>
    Pseudo
</Link>
```

__Важно:__ у всех типов `MetrikaLink` отсутствует prop `href`, вместо его нужно использовать `to`.

## `useOnClickWithClosePopups`

Хук который стоит использовать для решения проблемы закрытия у поппапов при нажатии на ссылку:

```jsx
import React, { FC } from 'react';
const MyComponent: FC = ({ onClick }) => {
    const onClickWithClosePopups = useOnClickWithClosePopups(onClick);
    return (
        <a
            href="/list"
            onClick={onClickWithClosePopups}
        >
            list
        </a>
    );
};
```

__Важно:__ данный хук уже используется в `Link` и `ExternalLink`, так что при использовании Метрика ссылок, использовать
`useOnClickWithClosePopups` напрямую нету необходимости.

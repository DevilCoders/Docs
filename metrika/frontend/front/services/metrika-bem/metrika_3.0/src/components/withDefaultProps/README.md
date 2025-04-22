В TS нет нормального способа указать дефолтные пропсы без бойлерплейта

```tsx
import * as React from 'react';
import { ComponentType, SFC } from 'react';
import { withDefaultProps } from 'components/withDefaultProps/withDefaultProps';

interface MyComponentProps {
    size: 'xs' | 's' | 'm';
    theme: 'action' | 'normal';
}

const MyComponent: SFC<MyComponentProps> = ({ size, theme }) => (
    <div>
        size is {size}, theme is {theme}
    </div>
);

// При опечатке в значении, например actionS вместо action
// TS выдаст ошибку
export default withDefaultProps(MyComponent, { theme: 'action' });

// использование
<MyComponent size="s" /> // size is s, theme is action (default)
<MyComponent size="s" theme="normal" /> // size is s, theme is normal
<MyComponent /> // ошибка, нет обязательного пропса size
<MyComponent size="s" theme="nenormal" /> // ошибка, theme должен быть "action" | "normal"
```

Чтобы объект с дефолтными пропсами задать через переменную, то ей нужно явно указать тип. Например так
```tsx
interface MyComponentProps {
    size: 'xs' | 's' | 'm';
    theme: 'action' | 'normal';
}
const defaultProps: Pick<MyComponentProps, 'theme'> = {
    theme: 'action';
};

export default withDefaultProps(MyComponent, defaultProps);
```

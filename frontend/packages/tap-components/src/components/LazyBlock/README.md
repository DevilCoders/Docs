# LazyBlock

Компонент для ленивой загрузки блока.

Принимает функцию получения данных и скелетон, который рисуется до момента отрисовки основного элемента.

## Пример использования

```typescript jsx
import React, { lazy, useState, useCallback } from 'react';
import { LazyBlock } from '@yandex-int/tap-components/LazyBlock';

import Skeleton from './components/Skeleton';
import api from './api';

const Component = lazy(() => import('./components/Component'));

const App: React.FC = () => {
    const [data, setData] = useState();
    const fetchData = useCallback(() => {
        api().then(res => setData(res));
    }, []);

    return  (
        <LazyBlock skeleton={<Skeleton />} fetchData={fetchData} >
            <Component data={data} />
        </LazyBlock>
    );
};

export { MyComponent };
```

## Пример

{{%story:::tap-components-components-lazyblock--playground%}}

## Свойства

| Свойство   | Тип                  | Описание                    |
| ---------- | -------------------- | ----------------------------|
| children   | `React.ReactElement` | Компонент для рендера       |
| fetchData? | `() => void`         | Функция для загрузки данных |
| skeleton?  | `React.ReactElement` | Заглушка                    |

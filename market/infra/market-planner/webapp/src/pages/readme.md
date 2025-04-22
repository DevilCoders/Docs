# Страницы

При обращении к конкретному роуту приложения идет обращение в конфиг со списком роутов, выбирается страница, затем идет ее рендер. Встроенный роутинг не умеет в разделение роутов  по query-параметрам, поэтому такой роутинг придется произвести на уровне контроллера и рутовой вьюхи.

Страницы используют три основных компонента:

- Страничный контроллер (обычно файл index с походом в ресурсы за данными)
- Вьюха на React (обычно файл view с экспортом верстки)
- Рутовый атом (обычно файл в atoms/combined, подключающий атомы, которые могут использоваться на странице)

Для редиректов используется этот модуль.

## Как создать новую страницу

1. Создаем папку в `src/pages`, внутри папки создаем файлы:
```
index.ts
view.tsx
atoms/page.ts
atoms/combined.ts
types.ts
```

### Подготовка types.ts
В файле `types.ts` описываем основные декларации:
```typescript
import {DepartmentId} from '../../entities/department';
import {EmployeeId} from '../../entities/employee';

export type PageParams = {
    departmentId?: string,
};

export type PageState = {
    departmentId: DepartmentId | undefined,
    employeesIds: EmployeeId[],
};
```

Стоит обратить внимание, что сейчас у входных параметров страницы есть 1 источник -- это `Router`, он прокидывает в параметры страницы все `query` параметры из урла. Поэтому честно будет делать их опциональными.

### Подготовка index.ts
В файле `index.ts` описываем костяк:
```typescript
import {PageFactory} from '../../lib/page';
import {View} from './view';
import {CombinedPageAtom} from './atoms/combined';
import {PageAtom, preparePageAtom} from './atoms/page';
```

```typescript
export interface MyPageParams {
    foo?: string;
    bar?: string;
}
```

Далее описываем функцию загрузки данных, на вход она получает входные параметры, а на выходе должна отдавать подготовленный `state` для всех нужных нам атомов.
```typescript
const loadData = (props: MyPageParams) => Promise.resolve({
    ...(preparePageAtom({
        foo: props.foo,
        bar: props.bar,
    })),
});
```

При помощи фабрики создаем экземпляр контроллера страницы и экспортируем его:
```typescript
export const MyPage = new PageFactory(NotFoundPageView, loadData, pageAtom);
```

### Набор атомов

Смотрим на продуктовую постановку задачи и директорию `entities`. Никакая бизнес логика не должна быть реализованна там, корневые сущности максимально абстрактны. Понимаем, какой набор атомов нужен для данной страницы, если нужна новая сущность или функционал -- имплементируем.
Например, нужно сходить в Api-ручку за данными. После нормализации мы получим два поля: `result` и `collections`. Корневые атомы сущностей в этом случае могут хранить коллекции (как абсолютно абстрактные данные), а набор айдишников result -- страничный атом.

`./atoms/page`
```typescript
import {declareAtom} from '@reatom/core';

import {PageState} from '../types';
import {prepareAtom} from '../../../entities/utils';

export const PageAtom = declareAtom<PageState>(
    'PageAtom',
    {
        foo: 'bar',
    },
    () => {}
);

export const preparePageAtom = prepareAtom<State>(PageAtom);
```

Все атомы, используемые на странице нужно обязательно поместить в массив и обернуть функцией `combine`, создав _рутовый страничный атом_.
```typescript
import {combine} from '@reatom/core';

import {fooAtom} from '../../../entities/foo';
import {barAtom} from '../../../entities/bar';
import {PageAtom} from './page';

export const CombinedPageAtom = combine([
    fooAtom,
    barAtom,
    PageAtom,
]);
```

### Подготовка View

```typescript jsx
import React from 'react';

export const View = () => { return (<SomeJsx /> };
```

Используя код из `src/containers` и `src/components` (и добавляя свои страничные контейнеры и компоненты), реализовываем верстку.

### Добавление в конфиг
В файле `src/configs/receiving.ts`:

Импортируем наш контроллер:
```typescript
import {MyPage} from '../pages/myPage';
```

В конфиг добавляем:
```typescript
myPage: {
    path: '/myPage',
    params: {
        permanentParam: 'bar',
    },
    controller: MyPage,
},
```

Теперь для того, чтобы построить урл для данной страницы можно использовать:
```typescript jsx
import {buildUrl} from '../../app/router';

const url = buildUrl('myPage', {});
```


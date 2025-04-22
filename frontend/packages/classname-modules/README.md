# classname-modules

Инструмент для составления CSS классов по бему с поддержкой css-modules

## Установка

`npm i @yandex-int/classname-modules`

## Использование

```ts
// Block/cn.ts
import { cn } from '@yandex-int/classname-modules';

import styles from './Block.module.css';

export const cnBlock = cn('Block', styles);
```

```tsx
// Block/Block.tsx
import React from 'react';

import { Element } from './Element/Element';

export const Block = ({ className, type, visible }) => (
  <div className={cnBlock({ type, visible }, [className])}>
    <Element className={styles['Block-Item']} color="red" />
    <Element className={styles['Block-Item']} color="red" />
    <Element className={styles['Block-Item']} color="red" />
  </div>
);
```

```css
/* Block/Block.module.css */
.Block {
    display: none;

    width: 200px;
    height: 200px;
}

.Block_visible {
    display: block;
}

.Block_type_default {
    background-color: blue;
}

.Block-Item:not(:first-child) {
    margin-top: 16px;
}
```

```tsx
// Block/Element/BlockElement.tsx
import React from 'react';

import { cnBlock as cn } from '../cn';

import styles from './BlockElement.module.css';

const cnBlock = cn.setStyles(styles);

export const BlockElement = ({ className, color }) => <div className={cnBlock('Element', { color }, [className])} />;
```

```css
/* Block/Element/BlockElement.module.css */
.Block-Element {
    width: 50px;
    height: 50px;
}

.Block-Element_color_red {
    background-color: red;
}
```

## Api

Api аналогичное [@bem-react/classname](https://github.com/bem/bem-react/tree/master/packages/classname)
За исключением того, что нет исключения дублирующих блока / элемента миксов

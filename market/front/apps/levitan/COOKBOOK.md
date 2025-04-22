# Levitan Cookbook

## React

### Определение ref компонентов

Свойство для передачи `ref` в компоненте в Левитане принято определяться как `$ref`.

Например:

```js
import React, {type Ref, type Node} from 'react'

type Props = {
    $ref: Ref<'button'>,
    children: Node,
}

const Button = ({$ref, children}: Props) => <button ref={$ref}>{children}</button>
```

Это соглашение позволяет удобно композировать компоненты, HOC и их пропсы, без необходимости контролировать непосредственно `ref` свойство. Однако для конечного внешнего интерфейса может быть удобно определить компонент с помощью [React.forwardRef](https://reactjs.org/docs/forwarding-refs.html), что можно сделать, к примеру, таким образом:

```js
const MyButton = React.forwardRef((props, ref) => Button({$ref: ref, ...props}))
```

#### ref для reshadow-элементов (кастомных элементов)

В случае, если необходимо передать `ref` [кастомному элементу](https://reshadow.dev/concepts#elements), нужно определить тип через `Ref<''>`, например:

```js
import React, {type Ref, type Node} from 'react'
import styled from 'reshadow'

type Props = {
    $ref: Ref<''>,
    children: Node,
    ...,
}

const Grid = ({$ref, styles, ...}: Props) => styled(styles)(
    <container ref={$ref}>
        ...
    </container>
)
```

В таком случае тип элемента в `ref` будет определен как `HTMLElement`, который и соответствует кастомному элементу во `flow`.

### Event handlers

Для обработки событий используются хендлеры с 2мя аргументами - ниболее часто испольуемое свойство и Event.

```typescript
import {TextField} from '@yandex-levitan/b2b'

export const MyComp = () => {
    const handler = (text: string, event: Event): void => {}
    //                     ^^^^^^         ^^^^^

    return <TextField onChange={handler} value="" />
}
```

## CSS

Общие договорённости по работе со стилями

### focus-ring

По умолчанию все компоненты с взаимодействиями при состоянии сфокусированности не подсвечиваются. Для того что бы они начали нужно начать навигироваться с помощью клавиатуры, а именно начать пользоваться <kbd>tab</kbd> или <kbd>shift</kbd><kbd>tab</kbd>. В этот момент включится режим навигации с помощью клавиатуры и компоненты должны обрести `focus-ring`. Для объявления стилей в режиме навигации с клавиатуры нужно использовать `focus-ring-on` миксин из `@yandex-levitan/core/styles/utils`. Смотри пример

```css
@resolve '@yandex-levitan/core/styles/mixins/utils';

/* default styles */
button:focus {
    outline: none;
    box-shadow: none;
}

/* keyboard-navigation-mode */
@mixin focus-ring-on {
    & button:focus {
        box-shadow: 0 0 0 1px $yellow, inset 0 0 0 1px $yellow;
    }
}
```

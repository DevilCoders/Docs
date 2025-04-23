Компонент для отображения вектографики, реагирующего на изменение Темы.

### Свойства компонента Vector2

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `icon` | Заимпортированная иконка | Допустимые размеры `m` |
| `view` | `alert` `disable` `ghost` `primary` `secondary` `success` `system` `warning` | Цвет отображения иконки |
| `size` | `m` | Размер иконки |

```jsx
const Cash = require('./cash/m').default;
const Cashback = require('./cashback/m').default;
const Connect = require('./connect/m').default;
const Discount = require('./discount/m').default;

<React.Fragment>
    <Vector2 icon={Cash} view='primary' size='m' />
    <Vector2 icon={Cashback} view='secondary' size='m' />
    <Vector2 icon={Connect} view='success' size='m' />
    <Vector2 icon={Discount} view='warning' size='m' />
</React.Fragment>
```

#### Использование с другой Темой

``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

const Cash = require('./cash/m').default;
const Cashback = require('./cashback/m').default;
const Connect = require('./connect/m').default;
const Discount = require('./discount/m').default;

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

<ThemedBackground>
    <Vector2 icon={Cash} view='primary' size='m' />
    <Vector2 icon={Cashback} view='secondary' size='m' />
    <Vector2 icon={Connect} view='success' size='m' />
    <Vector2 icon={Discount} view='warning' size='m' />
</ThemedBackground>
```

### Добавление иконки
Для того, чтобы добавить новую иконку, нужно добавить его в директорию `assets/vector2` с именем `vector2_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:vector2-config` и `generate:vector2-components`, затем иконки автоматически сгенерируются.

### Список всех иконок
```js noeditor
const AllVector2 = require('../../styleguide/components/AllVector2').default;

<AllVector2 />
```

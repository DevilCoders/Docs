Компонент для отображения иконок, реагирующих на изменение Темы.

### Свойства компонента Placeholder2 ###

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `icon` | Заимпортированная иконка. Допустымие размеры `m` `l` | Иконка |
| `view` | `alert` `brand` `ghost` | Цвет отображения иконки |

``` jsx
const PieM = require('./pie/m').default;
const PieL = require('./pie/l').default;

<div>
	<Placeholder2 icon={PieM} view="brand"/>
	<Placeholder2 icon={PieL} view="brand"/>
</div>
```

``` jsx
const OperatorM = require('./operator/m').default;

<div>
	<Placeholder2 icon={OperatorM} view="alert"/>
	<Placeholder2 icon={OperatorM} view="brand"/>
	<Placeholder2 icon={OperatorM} view="ghost"/>
</div>
```

#### Использование с другой Темой

``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

const SearchM = require('./search/m').default;
const SearchL = require('./search/l').default;

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

<ThemedBackground>
    <Placeholder2 icon={SearchM} view="alert"/>
    <Placeholder2 icon={SearchM} view="brand"/>
    <Placeholder2 icon={SearchM} view="ghost"/>
</ThemedBackground>
```

### Добавление иконки

Для того, чтобы добавить новую иконку, нужно добавить её в корневую директорию `assets/placeholder2` с именем `placeholder2_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:placeholder2-config` и иконки автоматически сгенерируются.

### Список всех иконок
```js noeditor
const AllPlaceholder2 = require('../../styleguide/components/AllPlaceholder2').default;

<AllPlaceholder2 />
```

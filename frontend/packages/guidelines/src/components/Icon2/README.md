Компонент для отображения иконок, реагирующих на изменение Темы.

### Свойства компонента Icon2 ###

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `icon` | Заимпортированная иконка. Допустымие размеры `s` `m` | Иконка |
| `round` | `alert` `success` `system` `warning` | Тип круглого фона |
| `view` | `alert` `brand` `disable` `ghost` `primary` `secondary` `success` `system` `warning` | Цвет отображения иконки |

``` jsx
const FingerprintS = require('./fingerprint/s').default;
const FingerprintM = require('./fingerprint/m').default;

<div>
	<Icon2 icon={FingerprintS} view="brand"></Icon2>
	<Icon2 icon={FingerprintM} view="brand"></Icon2>
</div>
```

``` jsx
const FingerprintM = require('./fingerprint/m').default;

<div>
	<Icon2 icon={FingerprintM} view="alert"></Icon2>
	<Icon2 icon={FingerprintM} view="disable"></Icon2>
	<Icon2 icon={FingerprintM} view="ghost"></Icon2>
	<Icon2 icon={FingerprintM} view="primary"></Icon2>
	<Icon2 icon={FingerprintM} view="secondary"></Icon2>
	<Icon2 icon={FingerprintM} view="success"></Icon2>
	<Icon2 icon={FingerprintM} view="system"></Icon2>
	<Icon2 icon={FingerprintM} view="warning"></Icon2>
</div>
```

``` jsx
const FingerprintM = require('./fingerprint/m').default;

<div>
	<Icon2 icon={FingerprintM} view="primary" round="alert"></Icon2>
	<Icon2 icon={FingerprintM} view="primary" round="success"></Icon2>
	<Icon2 icon={FingerprintM} view="primary" round="system"></Icon2>
	<Icon2 icon={FingerprintM} view="primary" round="warning"></Icon2>
</div>
```

#### Использование с другой Темой

``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

const FingerprintS = require('./fingerprint/s').default;
const FingerprintM = require('./fingerprint/m').default;

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

<ThemedBackground>
    <Icon2 icon={FingerprintM} view="alert"></Icon2>
    <Icon2 icon={FingerprintM} view="disable"></Icon2>
    <Icon2 icon={FingerprintM} view="ghost"></Icon2>
    <Icon2 icon={FingerprintM} view="primary"></Icon2>
    <Icon2 icon={FingerprintM} view="secondary"></Icon2>
    <Icon2 icon={FingerprintM} view="success"></Icon2>
    <Icon2 icon={FingerprintM} view="system"></Icon2>
    <Icon2 icon={FingerprintM} view="warning"></Icon2>
</ThemedBackground>
```

``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

const FingerprintS = require('./fingerprint/s').default;
const FingerprintM = require('./fingerprint/m').default;

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

<ThemedBackground>
    <Icon2 icon={FingerprintM} view="primary" round="alert"></Icon2>
    <Icon2 icon={FingerprintM} view="primary" round="success"></Icon2>
    <Icon2 icon={FingerprintM} view="primary" round="system"></Icon2>
    <Icon2 icon={FingerprintM} view="primary" round="warning"></Icon2>
</ThemedBackground>
```

### Добавление иконки

Для того, чтобы добавить новую иконку, нужно добавить её в корневую директорию `assets/icon2` с именем `icon2_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:icons2-config` и иконки автоматически сгенерируются.

### Список всех иконок
```js noeditor
const AllIcons2 = require('../../styleguide/components/AllIcons2').default;

<AllIcons2 />
```

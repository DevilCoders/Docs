Компонент для отображения иконок платформ, для маркировки карточек и платежных блоков.

### Свойства компонента PlatformIcon

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `icon` | Заимпортированная иконка. Допустымие размеры `m` `l` | Иконка |
| `view` | `primary` `ghost` | Цвет отображения иконки |

#### Для использования со свойством view:

``` jsx
const GooglePayM = require('./google-pay/m').default;
const GooglePayL = require('./google-pay/l').default;

<div>
	<PlatformIcon icon={GooglePayM} view='primary'></PlatformIcon>
	<PlatformIcon icon={GooglePayL} view='primary'></PlatformIcon>
	<PlatformIcon icon={GooglePayM} view='ghost'></PlatformIcon>
	<PlatformIcon icon={GooglePayL} view='ghost'></PlatformIcon>
</div>
```

#### Для использования brand цвета:

``` jsx
const GooglePayBrandM = require('./google-pay-brand/m').default;
const GooglePayBrandL = require('./google-pay-brand/l').default;

<div>
	<PlatformIcon icon={GooglePayBrandM}></PlatformIcon>
	<PlatformIcon icon={GooglePayBrandL}></PlatformIcon>
</div>
```

#### Использование с другой Темой

``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

const GooglePayM = require('./google-pay/m').default;
const GooglePayL = require('./google-pay/l').default;

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

<ThemedBackground>
    <PlatformIcon icon={GooglePayM} view='primary'></PlatformIcon>
    <PlatformIcon icon={GooglePayL} view='primary'></PlatformIcon>
    <PlatformIcon icon={GooglePayM} view='ghost'></PlatformIcon>
    <PlatformIcon icon={GooglePayL} view='ghost'></PlatformIcon>
</ThemedBackground>
```

### Добавление иконки

Для того, чтобы добавить новую иконку, нужно добавить его в директорию `icons/platform-icon` с именем `platform-icon_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:platform-icon-config` и `generate:platform-icon-components`, затем иконки автоматически сгенерируются.

### Список всех иконок
```js noeditor
const AllPlatformIcon = require('../../styleguide/components/AllPlatformIcon').default;

<AllPlatformIcon />
```

Компонент иконок социальных сетей и мессенджеров, реагирующий на изменение Темы

### Свойства компонента SocialIcon2

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `icon` | Заимпортированная иконка. Допустымие размеры `m` | Иконка |
| `view` | `alert` `disable` `ghost` `primary` `secondary` `success` `system` `warning` | Цвет отображения иконки |
| `round` | `alert` `brand` `disable` `ghost` `primary` `secondary` `success` `system` `warning` | Тип скругления |

#### Для использования со свойством view:

``` jsx
const Instagram = require('./instagram/m').default;

<div>
	<SocialIcon2 icon={Instagram} size='m' view='alert'></SocialIcon2>
	<SocialIcon2 icon={Instagram} size='m' view='disable'></SocialIcon2>
	<SocialIcon2 icon={Instagram} size='m' view='ghost'></SocialIcon2>
	<SocialIcon2 icon={Instagram} size='m' view='primary'></SocialIcon2>
	<SocialIcon2 icon={Instagram} size='m' view='secondary'></SocialIcon2>
	<SocialIcon2 icon={Instagram} size='m' view='success'></SocialIcon2>
	<SocialIcon2 icon={Instagram} size='m' view='system'></SocialIcon2>
	<SocialIcon2 icon={Instagram} size='m' view='warning'></SocialIcon2>
</div>
```

#### Для использования brand цвета:

``` jsx
const InstagramBrand = require('./instagram-brand/m').default;
const TwitterBrand = require('./twitter-brand/m').default;

<div>
	<SocialIcon2 icon={InstagramBrand} size='m'></SocialIcon2>
	<SocialIcon2 icon={TwitterBrand} size='m'></SocialIcon2>
</div>
```

```jsx
const Twitter = require('./twitter/m').default;

<div>
	<SocialIcon2 icon={Twitter} size='m' round='alert'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='brand'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='disable'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='ghost'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='primary'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='secondary'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='success'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='system'></SocialIcon2>
	<SocialIcon2 icon={Twitter} size='m' round='warning'></SocialIcon2>
</div>
```

#### Использование с другой Темой
``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

const Instagram = require('./instagram/m').default;

<ThemedBackground>
    <SocialIcon2 icon={Instagram} size='m' view='alert'></SocialIcon2>
    <SocialIcon2 icon={Instagram} size='m' view='disable'></SocialIcon2>
    <SocialIcon2 icon={Instagram} size='m' view='ghost'></SocialIcon2>
    <SocialIcon2 icon={Instagram} size='m' view='primary'></SocialIcon2>
    <SocialIcon2 icon={Instagram} size='m' view='secondary'></SocialIcon2>
    <SocialIcon2 icon={Instagram} size='m' view='success'></SocialIcon2>
    <SocialIcon2 icon={Instagram} size='m' view='system'></SocialIcon2>
    <SocialIcon2 icon={Instagram} size='m' view='warning'></SocialIcon2>
</ThemedBackground>
```

``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

const Twitter = require('./twitter/m').default;

<ThemedBackground>
    <SocialIcon2 icon={Twitter} size='m' round='alert'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='brand'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='disable'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='ghost'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='primary'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='secondary'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='success'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='system'></SocialIcon2>
    <SocialIcon2 icon={Twitter} size='m' round='warning'></SocialIcon2>
</ThemedBackground>
```

### Добавление иконки

Для того, чтобы добавить новую иконку, нужно добавить его в директорию `assets/social-icon2` с именем `social-icon2_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:social-icon2-config` и `generate:social-icon2-components`, затем иконки автоматически сгенерируются.

### Список всех иконок
```js noeditor
const AllSocialIcon2 = require('../../styleguide/components/AllSocialIcon2').default;

<AllSocialIcon2 />
```

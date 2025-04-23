Компонент для отображения категорий товаров и услуг. Используется для обобщения или в качестве заглушки (если отсутствует логотип партнёра).

### Свойства компонента CategoryLogo

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `icon` | Заимпортированная иконка. Допустымие размеры `s` `m` `l` | Иконка |
| `view` | `action` `ghost` | Цвет отображения иконки |

``` jsx
const AutoPaymentsS = require('./auto-payments/s').default;
const AutoPaymentsM = require('./auto-payments/m').default;
const AutoPaymentsL = require('./auto-payments/l').default;

<div>
	<CategoryLogo icon={AutoPaymentsL} view="action"></CategoryLogo>
	<CategoryLogo icon={AutoPaymentsM} view="action"></CategoryLogo>
	<CategoryLogo icon={AutoPaymentsS} view="action"></CategoryLogo>
	<CategoryLogo icon={AutoPaymentsL} view="ghost"></CategoryLogo>
	<CategoryLogo icon={AutoPaymentsM} view="ghost"></CategoryLogo>
	<CategoryLogo icon={AutoPaymentsS} view="ghost"></CategoryLogo>
</div>
```

#### Использование с другой Темой

``` jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

const AutoPaymentsS = require('./auto-payments/s').default;

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	padding: 10px;
	background: var(--color-bg-default);
`;

<ThemedBackground>
    <CategoryLogo icon={AutoPaymentsS} view="action"></CategoryLogo>
    <CategoryLogo icon={AutoPaymentsS} view="ghost"></CategoryLogo>
</ThemedBackground>
```


### Добавление иконки

Для того, чтобы добавить новую иконку, нужно добавить её в корневую директорию `assets/category-logo` с именем `category_logo_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:category-logo-config` и иконки автоматически сгенерируются.

### Список всех иконок
```js noeditor
const AllCategoryLogo = require('../../styleguide/components/AllCategoryLogo').default;

<AllCategoryLogo />
```

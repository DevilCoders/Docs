Компонент для отображения бейджей сторов мобильных приложений.

### Свойства компонента StoreBadge

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `icon` | Заимпортированный бейдж. Допустымие размеры `m` | Бейдж |
| `size` | `m` | Размер |
| `view` | `primary` | Цвет отображения бейджа |

```jsx
const {default: styled} = require('styled-components');

const AppStore = require('./app-store/m').default;
const GooglePlay = require('./google-play/m').default;

// Контейнер для StoreBadge, добавляет отступы
const Background = styled.div`
	& > svg {
		margin-right: 8px;
	}
`;

<Background>
	<StoreBadge
		icon={AppStore}
		view='primary'
	/>
	<StoreBadge
		icon={GooglePlay}
		view='primary'
	/>
</Background>
```

#### Использование с другой Темой

```jsx
const {default: styled} = require('styled-components');
const {colorYamoneyInverse} = require('../CSSVariables');

const AppStore = require('./app-store/m').default;
const GooglePlay = require('./google-play/m').default;

// Темный фон, чтобы было видно inverse версию
const ThemedBackground = styled.div`
	${colorYamoneyInverse}
	& > svg {
		margin-right: 8px;
	}
	padding: 8px;
	background: var(--color-bg-default);
`;

<ThemedBackground>
    <StoreBadge
        icon={AppStore}
        view='primary'
    />
    <StoreBadge
        icon={GooglePlay}
        view='primary'
    />
</ThemedBackground>
```


### Добавление иконки

Для того, чтобы добавить новый бейдж, нужно добавить его в директорию `assets/store-badge` с именем `store-badge_name_НАЗВАНИЕ_РАЗМЕР.svg`. При коммите запустится таск `generate:store-badge-config` и иконки автоматически сгенерируются.

### Список всех бейджей
```js noeditor
const AllStoreBadge = require('../../styleguide/components/AllStoreBadge').default;

<AllStoreBadge />
```

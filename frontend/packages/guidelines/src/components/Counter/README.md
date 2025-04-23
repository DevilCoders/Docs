Компонент счетчиков, выводиться для отображения количества чего-либо в смысловом блоке (оповещения, события, итд).

### Свойства компонента Counter

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `size` | `s` `xs` | Размер |
| `view` | `alert` |  Фон |

``` jsx
<div>
	<Counter size='xs' view='alert'>
		1
	</Counter>
	<Counter size='s' view='alert'>
		1
	</Counter>
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
	<ThemedBackground>
        <Counter size='xs' view='alert'>
            1
        </Counter>
        <Counter size='s' view='alert'>
            1
        </Counter>
	</ThemedBackground>
```

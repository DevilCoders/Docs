Инпут для фильтров сравнения строк

behavior = undefined
Неконтроллируемый инпут
```jsx
const { noop } = require('lodash');

<ComparableInput onChange={noop} />
```

behavior = 'contraction'
Если введённое значение не является числом, список возможных опций сокращается
```jsx
const { noop } = require('lodash');

<ComparableInput onChange={noop} behavior="contraction" />
```

behavior = 'restrictToUnsignedInt'
Если введённое значение не является целым числом, не вызывается onChange
```jsx
<ComparableInput onChange={() => console.log('change')} behavior="restrictToUnsignedInt" />
```

behavior = 'restrictToNumber'
Если введённое значение не является числом, не вызывается onChange
```jsx
const { noop } = require('lodash');

<ComparableInput onChange={noop} behavior="restrictToNumber" />
```

Диапазон значений
condition: RangeConditionValue
```jsx
const { noop } = require('lodash');

const condition = { operator: '<>', value: ['10', '20'] };

<ComparableInput onChange={noop} condition={condition} />
```
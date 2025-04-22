# FatalError

Компонент для отображения страничных ошибок по http-кодам.

## Примеры использования

### Пример 1. Для кода ошибки: 400
```jsx
import {Provider} from 'react-redux';
<Provider store={{}}>
    <FatalError code="400" />
</Provider>
```

### Пример 2. Для кода ошибки: 403
```jsx
import {Provider} from 'react-redux';
<Provider store={{}}>
    <FatalError code="403" />
</Provider>
```

### Пример 3. Для кода ошибки: 404
```jsx
import {Provider} from 'react-redux';
<Provider store={{}}>
    <FatalError code="404" />
</Provider>
```

### Пример 4. Для кода ошибки: 500
```jsx
import {Provider} from 'react-redux';
<Provider store={{}}>
    <FatalError code="500" />
</Provider>
```

### Пример 5. Без кнопки возврата для кода ошибки: 400
```jsx
import {Provider} from 'react-redux';
<Provider store={{}}>
    <FatalError code="400" showBackButton={false} />
</Provider>
```

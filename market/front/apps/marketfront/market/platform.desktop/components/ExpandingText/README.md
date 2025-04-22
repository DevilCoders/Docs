# ExpandingText

Раскрывающийся блок текста

Отображается с кнопками "Читать далее"/"Свернуть", если текст превышает заданную константу,
которая может приниматься из пропсов, по дефолту 300 символов.


Пример использования:
```jsx
const ExpandingText = require('@self/platform/components/ExpandingText').default;

const text = 'test test test test test test test test test test test test test test test test test test test test test';
const maxLength = 50;

<ExpandingText
    text={text}
    maxLength={maxLength}
/>

```

# ColorSet

Кружочки с цветами продукта

Пример использования:
```jsx
const ColorSet = require('@self/platform/components/ColorSet').default;
const {filter} = require('@self/platform/components/ColorSet/__fixtures__');

<ColorSet
    filter={filter}
    size="xs"
/>
```

С ограничением по цветам:
```jsx
const ColorSet = require('@self/platform/components/ColorSet').default;
const {filter} = require('@self/platform/components/ColorSet/__fixtures__');

<ColorSet
    filter={filter}
    maxColorsCount={2}
    size="m"
/>
```

С ограничением по цветам и короткой ссылкой:
```jsx
const ColorSet = require('@self/platform/components/ColorSet').default;
const {filter} = require('@self/platform/components/ColorSet/__fixtures__');

<ColorSet
    filter={filter}
    maxColorsCount={2}
    shortShowMoreLink
    size="l"
/>
```

С текстовым описанием цветов:
```jsx
const ColorSet = require('@self/platform/components/ColorSet').default;
const {filter} = require('@self/platform/components/ColorSet/__fixtures__');

<ColorSet
    filter={filter}
    withText
    size="l"
/>
```

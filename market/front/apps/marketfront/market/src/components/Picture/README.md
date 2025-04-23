# Picture

Аналог n-picture из yate

Выбирает картинку нужного размера из переданного массива thumbnails и возвращает тег img

Пример использования:
```jsx
const Picture = require('@self/platform/components/Picture').default;
const {thumbnails} = require('@self/platform/components/Picture/__fixtures__');

<Picture
    thumbnails={thumbnails}
    size={200}
    hasTitle
    hidpi
/>
```

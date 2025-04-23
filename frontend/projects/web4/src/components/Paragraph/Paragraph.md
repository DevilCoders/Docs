# Paragraph

Текстовый абзац. Нужен, чтобы разделять крупные массивы текста отступом.

Отступ появится у двух и более абзацев, расположенных рядом.

## Usage

Импортировать `paragraphCn` и миксовать его к своим компонентам.

```js
import { paragraphCn } from '../components/Paragraph/Paragraph';

export const MyComponent = () => (
    <div>
        <div classNmae={paragraphCn}>Paragraph 1</div>
        <div classNmae={paragraphCn}>Paragraph 2</div>
        <div classNmae={paragraphCn}>Paragraph 3</div>
    </div>
);
```

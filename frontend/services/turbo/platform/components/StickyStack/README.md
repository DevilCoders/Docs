## StickyStack

Блок для отображения «залипающего» контента.

```ts
interface IProps {
    children: React.Child[]; // Элементы, которые распределяются по блоку
    step?: number; // Интервал, отведенный для отображения каждого из них
    mixedContent?: Array<{ // Пока не готовы дочерние компоненты на реакте, рендерим дерево через dangerouslySetInnerHTML...
        __html: string,
    }>
}
```

**Примечание**:

- Блок использует только `position: sticky`
- Если `step` не указан, то блок с помощью `flex` распределяет пространство
- Потомки оборачиваются так: `<div class="sticky-stack__element"><div class="sticky-stack__element-content">any children</div></div>`, чтобы при скроле, блоки не наезжали друг на друга, а "вытесняли". Т.е. `sticky` устанавливается на `.sticky-stack__element .sticky-stack__element-content`
- На последний `.sticky-stack__element` устанавливается `sticky`, чтобы он остался до конца, если дальше пустота


## 😱

На данный момент, в проекте рендерится через bem -> html -> React

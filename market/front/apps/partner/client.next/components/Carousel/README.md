# Компонент карусели

## Использование
```tsx
<Carousel>
    <Item></Item>
    <Item></Item>
    <Item></Item>
    <Item></Item>
</Carousel>
```
```tsx
<Carousel threshold={0.6}>
    <Item></Item>
    <Item></Item>
    <Item></Item>
    <Item></Item>
</Carousel>
```

## Пропсы

```typescript
    type Props = {
        children: React.ReactElement | React.ReactElement[];
        // необходимо задавать, если в контейнер помещается ≤1 элемента.
        // Надо указать долю элемента который помещается (0 <= threshold <= 1)
        threshold?: number;
    }
```

## Логика работы

IntersectionObserver API следим за тем, какие дочерние элементы видимы и при нажатии на кнопки, скроллим к соответствующему невидимому элементу.
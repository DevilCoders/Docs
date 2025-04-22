# Замена свойства

Разные значения модификатора `size` компонента "Rating" используют числовое свойство `starSize` базовой реализации компонента:

``` tsx
export const RatingSizeM = withBemMod<IRatingSizeM, IRatingProps>(
    cnRating(),
    { size: 'm' },
    RatingBase => props => (
        <RatingBase starSize={16} {...props} />
    )
);
```

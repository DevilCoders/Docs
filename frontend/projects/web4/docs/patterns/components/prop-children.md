# Props.children

В базовой реализации компонента [CarouselControls](../../../src/components/CarouselControls) внутрь рендерится переданные в `props.children` React-ноды или генерируется контент по умолчанию:

``` tsx
export const CarouselControls: React.FC<ICarouselControlsProps> = ({ colored, children, items = [] }) => (
    <div className={cnCarouselControls({ theme, colored })}>
        {children || items.map(({ url, text }, i) => (
            <Link
                className={cnCarouselControls('Item')}
                key={i}
                url={url}
                theme="default">
                {text}
            </Link>
        ))}
    </div>
);
```

Под модификатором [theme_colored](../../../src/components/CarouselControls/_colored/CarouselControls_colored.tsx) в компоненте подменяется содержимое на цветные ссылки:

``` tsx
export const carouselControlsColored = withBemMod<ICarouselControlsColoredProps, ICarouselControlsProps>(
    cnCarouselControls(),
    { colored: true },
    ControlsColored => props => {
        const { items = [] } = props;

        return (
            <ControlsColored {...props}>
                {items.map(({ url, text }, i) => (
                    <Link
                        className={cnCarouselControls('Item')}
                        key={i}
                        url={url}
                        theme="colored">
                        {text}
                    </Link>
                ))}
            </ControlsColored>
        );
    });
```

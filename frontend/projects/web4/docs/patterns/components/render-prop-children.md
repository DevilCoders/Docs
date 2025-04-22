# Props.children как Render Prop

В базовой реализации компонента [Map](../../../src/components/Map) `props.children` - это [Render Prop](https://reactjs.org/docs/render-props.html), вызываемый с реальными размерами области под карту на клиенте:

``` tsx
export class Map extends React.Component<IMapProps, IMapState> {
    private ref = React.createRef<HTMLDivElement>();

    componentDidMount() {
        const currentRef = this.ref.current;
        if (currentRef) {
            this.setState({
                size: utils.calculateSize(currentRef)
            });
        }
    }

    render() {
        const { width, height } = this.state.size;

        return (
            <div className={cnMap()} style={{ width, height }}>
                {width && height && this.props.children({ width, height })}
            </div>
        );
    }
}
```

Под модификатором [type_static](../../../src/components/Map/_type/Map_type_static.tsx) в компонент подставляется статическая картинка нужных размеров:

``` tsx
export const MapTypeStatic = withBemMod<IMapProps>(
    cnMap(),
    { type: 'static' },
    MapBase => props => (
        <MapBase {...props}>{size => <Image url={getStaticImageUrl(size)} />}</MapBase>
    )
);
```

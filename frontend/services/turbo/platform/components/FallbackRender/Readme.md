# Хелпер для работы с компонентами, которым нужен fallback.

Например, асинхронно загружающиеся компоненты, которые могут не загрузиться (вроде рекламы).


Допустим, у нас есть компонент, который, по каким-либо причинам, может не загрузиться:
```
interface IProps {
    onFallback(): void;
}

class SomeComponent extends React.PureComponent<IProps> {
    componentDidMount() {
        const { onFallback } = this.props;

        setTimeout(() => {
            onFallback();
        }, 1000);
    }

    render() {
        return <div>Я загружаюсь...</div>;
    }
}
```

Используя `FallbackRender` мы можем обработать оба варианта загрузки
```
function ExampleBase() {
    return (
        <FallbackRender>
            {({ isFallback, onFallbackRender }) => {
                return isFallback ?
                    <div>Я покажусь, если SomeComponent не загрузится</div> :
                    <SomeComponent onFallback={onFallbackRender} />;
            }}
        </FallbackRender>
    );
}
```

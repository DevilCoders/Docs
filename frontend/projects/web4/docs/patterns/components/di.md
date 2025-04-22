# Реестры

### Хранение дополнительных функций/данных

В реестре кроме дочерних компонентов можно хранить дополнительные функции и данные, нужные компоненту.
Например можно хранить некоторые "предустановленные" props-ы или функции, используемые в хуках:

``` tsx
const ExamplePresenter: React.FC<IExampleProps> = props => {
    const { theme, showPopup, Link } = useRegistry<IExampleRegistry>(exampleCn);

    useEffect(() => {
        // вызываем в хуке функцию, взятую из реестра
        showPopup();
    });

    return (
        <div className={cnExample(undefined, [props.className])}>
            <Link
                theme={/* prop из реестра */ theme}
                href={props.url}
            >
                {/* обычный prop */ props.text}
            </Link>
        </div>
    );
};
```

### Зануление компонента

Отключение фавиконки в компоненте `Path` для платформы "desktop" когда-то было сделано через реестры.
В реестре под ключом `'Favicon'` находился `null`-компонент:

``` ts
pathRegistry.set(cnPath('Favicon'), () => null);
```

При этом в touch-phone версии реестра был компонент `Favicon`:

``` ts
import { Favicon } from '../../Favicon/Favicon@touch-phone';

pathRegistry.set(cnPath('Favicon'), Favicon);
```

Компонент `Path` всегда (на common-уровне) пытается отрендерить фавиконку:

``` ts
const PathPresenter: React.SFC<IPathProps> = ({ favicon, items }) => {
    const { Link, Favicon } = useRegistry<IPathRegistry>(cnPath());

    // для desktop Favicon === () => null,
    // поэтому фавиконки не будет даже если props-ы для нее есть

    return (
        <div className={cnPath()}>
            {favicon && <Favicon {...favicon} />}
            {items.map((item, i) => <Link key={i} text={item.text} url={item.url} />)}
        </div>
    );
};
```

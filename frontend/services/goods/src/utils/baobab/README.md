## Baobab

[Баобаб](https://wiki.yandex-team.ru/baobab/) — это система логирования деревьев страницы и происходящих в нём событий.

Для логирования используется библиотека [`@yandex-int/react-baobab-logger`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/frontend/packages/react-baobab-logger).

### `withBaobabPage`

HOC `withBaobabPage` используется для создания корневого baobab-компонета.
Каждая страница приложения создает свой корневой элемент путем оборачивания себя в HOC.

Пример: `src/pages/SearchPage/index.tsx`.

### `withBaobab`

HOC [`withBaobab`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/frontend/packages/react-baobab-logger/docs/architecture.md) используется для обертки компонентов.

Пример:
```ts
import { withBaobab, logClick } from '@yandex-int/react-baobab-logger';

interface IIconProps {
    onClick: () => void;
}

class IconBase extends React.Component<IIconProps> {
    render() {
        return <div onClick={this.props.onClick}/>;
    }
}

export const Icon = withBaobab({
    name: 'icon',
    attrs: {
        type: 'white'
    },
    events: {
        onClick: logClick(),
    }
})(IconBase);
```

Параметры `withBaobab`:
- `name` - название компонента;
- `attrs` - дополнтельные параметры компонента;
- `events` - события, которые необходимо залогировать.

Events бывают трех типов:
- `logClick()` - логирование кликов;
- `logScroll()` - логирование скролла;
- `logTech()` - логирование всех остальных событий.

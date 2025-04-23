# Утилиты для работы с qa-атрибутами в приложении

## IWithQaAttributes

`IWithQaAttributes` - интерфейс, который фиксирует как передаются атрибуты по дереву компонентов.

```tsx
import {IWithQaAttributes, prepareQaAttributes} from './qaAttributes';

interface IMyComponentProps extends IWithQaAttributes {
    // ...
}

const MyComponent = (props: IMyComponentProps) => {
    return <div {...prepareQaAttributes(props)}>content</div>;
};
```

## prepareQaAttributes

Чтобы не собирать значение qa атрибута вручную, существует функция `prepareQaAttributes`.
В качестве первого аргумента можно передавать строку, объект IObjectQAValue или объект с qa атрибутом.
В качестве второго аргумента можно передать кастомный qa атрибут, по умолчанию это 'data-qa'.

```ts
import {IWithQaAttributes} from './qaAttributes';

export type TQaProps = string | IObjectQAValue | IWithQaAttributes;

export interface IObjectQAValue {
    /**
     * Ключ элемента в списке
     */
    key?: string | number;
    /**
     * qa родителя
     */
    parent?: TQaProps;
    /**
     * qa текущего элемента
     */
    current?: TQaProps;
}
```

Component, также поддерживает такой объект в своем конструкторе.

Пример в коде приложения:

```tsx
// ...
import {prepareQaAttributes, IWithQaAttributes} from './qaAttributes';

interface IDateTimeProps extends IWithQaAttributes {
    time: string;
    date: string;
}

const DateTime = (props: IDateTimeProps) => {
    const {time, date} = props;

    return (
        <div {...prepareQaAttributes(props)}>
            <span {...prepareQaAttributes({parent: props, current: 'time'})}>
                {time}
            </span>
            <MagicComponent>
                <span
                    {...prepareQaAttributes({
                        parent: props,
                        current: {
                            parent: 'magic',
                            current: 'date',
                        },
                    })}
                >
                    {date}
                </span>
            </MagicComponent>
        </div>
    );
};

interface IDateTimeListProps {
    items: {date: string; time: string}[];
}

const DateTimeList = ({items}: IDateTimeListProps) => {
    return items.map((item, index) => {
        return (
            <DateTime
                key={index}
                date={item.date}
                time={item.time}
                {...prepareQaAttributes({key: index, current: 'dateTimeItem'})}
            />
        );
    });
};
```

Пример в тесте:

```js
class TestDateTime extends Component {
    constructor(browser, qa) {
        super(browser, qa);

        this.time = new Component(browser, {parent: qa, current: 'time'});

        this.date = new Component(browser, {parent: qa, current: 'date'});
    }
}

class TestPage extends Component {
    constructor(browser, qa) {
        super(browser, qa);

        this.dateTimeList = new ComponentArray(
            browser,
            'dateTimeItem',
            Component,
        );
    }
}
```

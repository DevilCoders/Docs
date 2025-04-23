Заголовок таблицы с сортировкой и подсказкой по ховеру

```(jsx)
<>
    <SortableHeader
        hint="Подсказка"
        direction="asc"
    >
        Визиты
    </SortableHeader>
    <br />
    <br />
    <SortableHeader
        hint="Подсказка"
        direction="desc"
    >
        Просмотры
    </SortableHeader>
    <br />
    <br />
    <SortableHeader
        hint="Подсказка"
    >
        Неактивный заголовок
    </SortableHeader>
</>
```

Кликабельный пример:
```(jsx)
const { WithState } = require('utils/WithState');
const headers = [
    { key: 'visits', name: 'Визиты', hint: 'Текст про визиты' },
    { key: 'views', name: 'Просмотры', hint: 'Текст про просмотры' },
];
const nextStateMap = {
    asc: 'desc',
    desc: 'asc',
};

<WithState state={{ key: headers[0].key, direction: 'asc' }}>
    {(state, setState) =>
        headers.map((headerInfo, index) => (
            <span key={index} style={{ display: 'inline-block', marginRight: '20px' }}>
                <SortableHeader
                    hint={headerInfo.hint}
                    direction={headerInfo.key === state.key && state.direction}
                    onSort={(direction) => {
                        if (state.key === headerInfo.key) {
                            setState({ direction: nextStateMap[direction] });
                        } else {
                            setState({ key: headerInfo.key, direction: 'asc' });
                        }
                    }}
                >
                    {headerInfo.name}
                </SortableHeader>
            </span>
        ))
    }
</WithState>
```

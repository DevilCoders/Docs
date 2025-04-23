Таблица для отчётов

Плоская, с возможность выбора, size=m
```(jsx)
const faker = require('faker/locale/ru');
const { ShowMore } = require('../ShowMore');
const _ = require('lodash');
const { WithState } = require('utils/WithState');

const crumbsItems = [
    {id: '1', title: faker.address.city()},
    {id: '2', title: faker.address.city()},
];

const crumbsItemsLong = [
    {title: 'Браузер'},
    {title: 'Версия браузера'},
    {title: 'Браузер'},
    {title: 'Версия браузера'},
    {title: 'Браузер'},
    {title: 'Версия браузера'},
    {title: 'Браузер'},
    {title: 'Версия браузера'},
    {title: 'Браузер'},
    {title: 'Версия браузера'},
].map((item, index) => ({...item, id: String(index)}));

const crumbsItemsWithSubtitleLong = crumbsItemsLong.map((item, index, arr) => ({
    ...item,
    subtitle: index === arr.length - 1 ? undefined : 'Chrome',
}));

const data = {
    header: {
        selected: false,
        color: 'grey',
        cells: [
            { id: 'visits', content: 'Визиты', sort: 'asc', hint: 'Подсказка для визитов' },
            { id: 'views', content: 'Просмотры', disableSort: true }
        ],
    },
    total: {
        id: 'total',
        selected: true,
        color: 'black',
        content: 'Итого и средние',
        cells: [
            { value: '144', subvalue: 'сумма' },
            { value: '1 144', subvalue: 'среднее' },
        ],
    },
    body: _.range(10).map((id) => ({
        id: String(id),
        selected: false,
        color: faker.internet.color(),
        content: faker.lorem.word(),
        cells: [
            { value: '144', subvalue: '13%' },
            { value: '1 144' },
        ],
    })),
    progress: false,
    totalRows: 20,
    offset: 10,
};

const loadMoreData = _.range(10, 20).map((id) => ({
    id: String(id),
    selected: false,
    color: faker.internet.color(),
    content: faker.lorem.word(),
    cells: [
        { value: '144', subvalue: '13%' },
        { value: '1 144' },
    ],
}));

<WithState state={data}>
{(state, setState) => (
    <div>
    <ReportTable
        type="flat"
        size="m"
        selectable={true}
        expandable={false}
        crumbs={crumbsItems}
        onSort={(direction, { id }) => {
            setState({
                ...state,
                header: {
                    ...state.header,
                    cells: state.header.cells.map((cell) => {
                        return {
                            ...cell,
                            sort: id === cell.id ? direction : undefined,
                        };
                    }),
                },
            });
        }}
        onRowPicked={(data) => {}}
        onRowSelect={(data) => {
            if (data.type === 'header') {
                const newHeaderStateChecked = !state.header.selected;
                setState({
                    ...state,
                    total: {
                        ...state.total,
                        selected: newHeaderStateChecked
                            ? state.total.selected
                            : false,
                    },
                    body: state.body.map((row, idx) => {
                        if (newHeaderStateChecked && idx < 5) {
                            return {
                                ...row,
                                selected: true,
                            };
                        }

                        return {
                            ...row,
                            selected: false,
                        };
                    }),
                    header: {
                        ...state.header,
                        selected: newHeaderStateChecked,
                    }
                });
            } else if (data.type === 'body') {
                setState({
                    ...state,
                    body: state.body.map((row) => {
                        if (row.id === data.row.id) {
                            return {
                                ...row,
                                selected: !row.selected,
                            };
                        }

                        return row;
                    }),
                });
            } else if (data.type === 'total') {
                setState({
                    ...state,
                    total: {
                        ...state.total,
                        selected: !state.total.selected,
                    },
                });
            }
        }}
        header={state.header}
        total={state.total}
        body={state.body}
    />
    {state.offset < state.totalRows && (
        <div style={{ textAlign: 'center', marginTop: '10px' }}>
            <ShowMore progress={state.progress} state={state.state} offset={state.offset} total={state.totalRows} onClick={() => {
                setState({...state, progress: true });
                setTimeout(() => {
                    setState({
                        ...state,
                        body: [
                            ...state.body,
                            ...loadMoreData,
                        ],
                        progress: false,
                        offset: 40,
                    });
                }, 1000);
            }} />
        </div>
    )}
    </div>
)}
</WithState>
```

Возможна сортировка по dimension
```(jsx)
const faker = require('faker/locale/ru');
const _ = require('lodash');
const { WithState } = require('utils/WithState');

const crumbsItems = [
    {id: '1', title: faker.address.city()}
];

const data = {
    header: {
        selected: false,
        color: 'grey',
        cells: [
            { id: 'visits', content: 'Визиты', sort: 'asc', hint: 'Подсказка для визитов' },
            { id: 'views', content: 'Просмотры', disableSort: true }
        ],
        dimensionSort: 'asc'
    },
    total: {
        id: 'total',
        selected: true,
        color: 'black',
        content: 'Итого и средние',
        cells: [
            { value: '144', subvalue: 'сумма' },
            { value: '1 144', subvalue: 'среднее' },
        ],
    },
    body: _.range(10).map((id) => ({
        id: String(id),
        selected: false,
        color: faker.internet.color(),
        content: faker.lorem.word(),
        cells: [
            { value: '144', subvalue: '13%' },
            { value: '1 144' },
        ],
    })),
    progress: false,
    totalRows: 20,
    offset: 10,
};

<WithState state={data}>
{(state, setState) => (
    <ReportTable
        type="flat"
        size="m"
        selectable={true}
        expandable={false}
        crumbs={crumbsItems}
        onRowPicked={(data) => {}}
        onDimensionSort={(data) => {
            setState({
                ...state,
                header: {
                        ...state.header,
                        dimensionSort: state.header.dimensionSort === 'asc' ? 'desc' : 'asc'
                    },
            });
        }}
        header={state.header}
        total={state.total}
        body={state.body}
    />
)}
</WithState>
```




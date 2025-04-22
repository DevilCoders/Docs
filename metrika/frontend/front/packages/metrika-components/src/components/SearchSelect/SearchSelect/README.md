Автокомплит с выбором элемента и подгрузкой данных.

Автокомплит состоит из статических блоков, которые можно обернуть в свои блоки для стилизации внутри проекта проекта.

Автокомплит имеет 2 представления:

→ <b>SearchSelect.SearchLayout</b> (Поле для поиска + Попап). 

```(jsx)
const { Button, Spin } = require('lego');
const { WithState } = require('utils/WithState');
const companyList = [
    {
        id: 1,
        label: 'ООО СЧАСТЛИВЫЙ СЛУЧАЙ',
    },
    {
        id: 2,
        label: 'ООО ЯНДЕКС.ОФД',
    },
    {
        id: 3,
        label: 'ОАО "АВТОКОЛОННА №1230"',
    },
    {
        id: 4,
        label: 'ООО "ТЕХНОСТРОЙ"',
    },
    {
        id: 5,
        label: 'ООО "СТРОЙКА"',
    },
    {
        id: 26,
        label: 'ООО "Компания №3"',
    },
    {
        id: 7,
        label: 'ИП Павлова Елена Антоновна',
    },
    {
        id: 8,
        label: 'ИП Богданова Елена Сергеевна',
    },
];
const renderItemLabel = ({ label, isPrevSelected }) => {
    return isPrevSelected ? <b>{label}</b> : label;
};

<>
    <WithState
        state={{
            items: companyList,
            selectedItem: null,
            state: '',
        }}
    >
        {(state, updateState) => (
            <SearchSelect
                onSelect={(selectedItem) => {
                    updateState({ selectedItem });
                }}
                items={state.items}
                selectedItem={state.selectedItem}
                loadData={(options) => {
                    updateState({
                        state: 'loading',
                    });

                    setTimeout(() => {
                        updateState({
                            state: 'success',
                            items: companyList.filter(
                                (item) =>
                                    item.label.indexOf(options.filter) >= 0,
                            ),
                        });
                    }, 500);
                }}
            >
                <SearchSelect.SearchLayout placeholder="Компания">
                    <SearchSelect.S.Section>
                        {state.state === 'loading' && (
                            <Spin progress size="xs" position="center" />
                        )}
                        {state.items.length ? (
                            <SearchSelect.List
                                renderItemLabel={renderItemLabel}
                            />
                        ) : (
                            <SearchSelect.S.Inner>
                                Ничего не найдено
                            </SearchSelect.S.Inner>
                        )}
                    </SearchSelect.S.Section>
                </SearchSelect.SearchLayout>
            </SearchSelect>
        )}
    </WithState>
</>;

```

→ <b>SearchSelect.SwitcherLayout</b> (Button + Попап). 

```(jsx)
const { Button, Spin } = require('lego');
const { WithState } = require('utils/WithState');
const companyList = [
    {
        id: 1,
        label: 'ООО СЧАСТЛИВЫЙ СЛУЧАЙ',
    },
    {
        id: 2,
        label: 'ООО ЯНДЕКС.ОФД',
    },
    {
        id: 3,
        label: 'ОАО "АВТОКОЛОННА №1230"',
    },
    {
        id: 4,
        label: 'ООО "ТЕХНОСТРОЙ"',
    },
    {
        id: 5,
        label: 'ООО "СТРОЙКА"',
    },
    {
        id: 26,
        label: 'ООО "Компания №3"',
    },
    {
        id: 7,
        label: 'ИП Павлова Елена Антоновна',
    },
    {
        id: 8,
        label: 'ИП Богданова Елена Сергеевна',
    },
];
<>
    <WithState
        state={{
            items: companyList,
            selectedItem: null,
            state: '',
        }}
    >
        {(state, updateState) => (
            <SearchSelect
                onSelect={(selectedItem) => {
                    updateState({ selectedItem });
                }}
                items={state.items}
                selectedItem={state.selectedItem}
                loadData={(options) => {
                    updateState({
                        state: 'loading',
                    });

                    setTimeout(() => {
                        updateState({
                            state: 'success',
                            items: companyList.filter(
                                (item) =>
                                    item.label.indexOf(options.filter) >= 0,
                            ),
                        });
                    }, 500);
                }}
            >
                <SearchSelect.SwitcherLayout text="Switcher Button">
                    <SearchSelect.S.Section>
                        <SearchSelect.S.Inner>
                            <SearchSelect.SearchInput placeholder="Поиск" />
                        </SearchSelect.S.Inner>
                    </SearchSelect.S.Section>

                    <SearchSelect.Total
                        renderTotal={(total) => {
                            return (
                                <SearchSelect.S.Section>
                                    <SearchSelect.S.Inner>
                                        <p>Всего: {total.total}</p>
                                    </SearchSelect.S.Inner>
                                </SearchSelect.S.Section>
                            );
                        }}
                    />

                    <SearchSelect.S.Section>
                        {state.state === 'loading' && (
                            <Spin progress size="xs" position="center" />
                        )}
                        {state.items.length ? (
                            <SearchSelect.List />
                        ) : (
                            <SearchSelect.S.Inner>
                                Ничего не найдено
                            </SearchSelect.S.Inner>
                        )}
                    </SearchSelect.S.Section>
                </SearchSelect.SwitcherLayout>
            </SearchSelect>
        )}
    </WithState>
</>;

```

Также компонент позволяет выводить вложенные списки.

```(jsx)
const { Button, Spin } = require('lego');
const { WithState } = require('utils/WithState');
const companyList = [
    {
        id: 1,
        label: 'Группа 1',
        items: [
            {
                id: 1,
                label: 'ООО СЧАСТЛИВЫЙ СЛУЧАЙ',
            },
            {
                id: 2,
                label: 'ООО ЯНДЕКС.ОФД',
            },
            {
                id: 3,
                label: 'ОАО "АВТОКОЛОННА №1230"',
            },
            {
                id: 4,
                label: 'ООО "ТЕХНОСТРОЙ"',
            },
            {
                id: 5,
                label: 'ООО "СТРОЙКА"',
            },
            {
                id: 26,
                label: 'ООО "Компания №3"',
            },
            {
                id: 7,
                label: 'ИП Павлова Елена Антоновна',
            },
            {
                id: 8,
                label: 'ИП Богданова Елена Сергеевна',
            },
        ],
    },
    {
        id: 2,
        label: 'Группа 2',
        items: [
            {
                id: 1,
                label: 'ООО СЧАСТЛИВЫЙ СЛУЧАЙ',
            },
            {
                id: 2,
                label: 'ООО ЯНДЕКС.ОФД',
            },
            {
                id: 3,
                label: 'ОАО "АВТОКОЛОННА №1230"',
            },
            {
                id: 4,
                label: 'ООО "ТЕХНОСТРОЙ"',
            },
            {
                id: 5,
                label: 'ООО "СТРОЙКА"',
            },
            {
                id: 26,
                label: 'ООО "Компания №3"',
            },
            {
                id: 7,
                label: 'ИП Павлова Елена Антоновна',
            },
            {
                id: 8,
                label: 'ИП Богданова Елена Сергеевна',
            },
        ],
    },
];

const renderItemLabel = ({ label, isPrevSelected }) => {
    return isPrevSelected ? <b>{label}</b> : label;
};

<>
    <WithState
        state={{
            items: companyList,
            selectedItem: null,
            state: '',
        }}
    >
        {(state, updateState) => (
            <SearchSelect
                closeOnSelect={false}
                onSelect={(selectedItem) => {
                    updateState({ selectedItem });
                }}
                items={state.items}
                selectedItem={state.selectedItem}
                loadData={(options) => {
                    updateState({
                        state: 'loading',
                    });

                    setTimeout(() => {
                        updateState({
                            state: 'success',
                            items: companyList.filter(
                                (item) =>
                                    item.label.indexOf(options.filter) >= 0,
                            ),
                        });
                    }, 500);
                }}
            >
                <SearchSelect.SearchLayout placeholder="Компания">
                    <SearchSelect.S.Section>
                        {state.state === 'loading' && (
                            <Spin progress size="xs" position="center" />
                        )}
                        {state.items.length ? (
                            <SearchSelect.GroupList
                                renderItemLabel={renderItemLabel}
                            />
                        ) : (
                            <SearchSelect.S.Inner>
                                Ничего не найдено
                            </SearchSelect.S.Inner>
                        )}
                    </SearchSelect.S.Section>

                    <SearchSelect.S.Section>
                        <SearchSelect.S.Inner>
                            <SearchSelect.Submit text={'OK'} />
                        </SearchSelect.S.Inner>
                    </SearchSelect.S.Section>
                </SearchSelect.SearchLayout>
            </SearchSelect>
        )}
    </WithState>
</>;
```

Автокомплит с множественным выбором элементов и подгрузкой данных.

Автокомплит состоит из статических блоков, которые можно обернуть в свои блоки для стилизации внутри проекта.

Автокомплит имеет 2 представления:

→ <b>MultiSearchSelect.SearchLayout</b> (Поле для поиска + Попап). 

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
            selectedItems: [],
            state: '',
        }}
    >
        {(state, updateState) => (
            <MultiSearchSelect
                onSubmit={(selectedItems) => {
                    updateState({ selectedItems });
                }}
                onReset={() => {
                    updateState({ selectedItems: [] });
                }}
                items={state.items}
                selectedItems={state.selectedItems}
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
                <MultiSearchSelect.SearchLayout placeholder="Компания">
                    <MultiSearchSelect.S.Section>
                        {state.state === 'loading' && (
                            <Spin progress size="xs" position="center" />
                        )}
                        {state.items.length ? (
                            <MultiSearchSelect.List
                                renderItemLabel={renderItemLabel}
                            />
                        ) : (
                            <MultiSearchSelect.S.Inner>
                                Ничего не найдено
                            </MultiSearchSelect.S.Inner>
                        )}
                    </MultiSearchSelect.S.Section>

                    <MultiSearchSelect.S.Section>
                        <MultiSearchSelect.S.Inner>
                            <MultiSearchSelect.Submit text={'Submit'} />
                            <MultiSearchSelect.Cancel text={'Cancel'} />
                            <MultiSearchSelect.Reset text={'Reset'} />
                        </MultiSearchSelect.S.Inner>
                    </MultiSearchSelect.S.Section>
                </MultiSearchSelect.SearchLayout>
            </MultiSearchSelect>
        )}
    </WithState>
</>;
```

→ <b>MultiSearchSelect.SwitcherLayout</b> (Button + Попап). 

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
            selectedItems: [],
            state: '',
        }}
    >
        {(state, updateState) => (
            <MultiSearchSelect
                onChange={(selectedItems) => {
                    updateState({ selectedItems });
                }}
                onReset={() => {
                    updateState({ selectedItems: [] });
                }}
                items={state.items}
                selectedItems={state.selectedItems}
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
                <MultiSearchSelect.SwitcherLayout text="Switcher Button">
                    <MultiSearchSelect.S.Section>
                        <MultiSearchSelect.S.Inner>
                            <MultiSearchSelect.SearchInput placeholder="Поиск" />
                        </MultiSearchSelect.S.Inner>
                    </MultiSearchSelect.S.Section>

                    <MultiSearchSelect.Total
                        renderTotal={(total) => {
                            return (
                                <MultiSearchSelect.S.Section>
                                    <MultiSearchSelect.S.Inner>
                                        <p>Всего: {total.total}</p>
                                        <p>Выбрано: {total.totalSelected}</p>
                                    </MultiSearchSelect.S.Inner>
                                </MultiSearchSelect.S.Section>
                            );
                        }}
                    />

                    <MultiSearchSelect.S.Section>
                        {state.state === 'loading' && (
                            <Spin progress size="xs" position="center" />
                        )}
                        {state.items.length ? (
                            <MultiSearchSelect.List />
                        ) : (
                            <MultiSearchSelect.S.Inner>
                                Ничего не найдено
                            </MultiSearchSelect.S.Inner>
                        )}
                    </MultiSearchSelect.S.Section>

                    <MultiSearchSelect.S.Section>
                        <MultiSearchSelect.S.Inner>
                            <MultiSearchSelect.Reset text={'Reset'} />
                        </MultiSearchSelect.S.Inner>
                    </MultiSearchSelect.S.Section>
                </MultiSearchSelect.SwitcherLayout>
            </MultiSearchSelect>
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
            selectedItems: [],
            state: '',
        }}
    >
        {(state, updateState) => (
            <MultiSearchSelect
                onSubmit={(selectedItems) => {
                    updateState({ selectedItems });
                }}
                onReset={() => {
                    updateState({ selectedItems: [] });
                }}
                items={state.items}
                selectedItems={state.selectedItems}
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
                <MultiSearchSelect.SearchLayout placeholder="Компания">
                    <MultiSearchSelect.S.Section>
                        {state.state === 'loading' && (
                            <Spin progress size="xs" position="center" />
                        )}
                        {state.items.length ? (
                            <MultiSearchSelect.GroupList
                                renderItemLabel={renderItemLabel}
                            />
                        ) : (
                            <MultiSearchSelect.S.Inner>
                                Ничего не найдено
                            </MultiSearchSelect.S.Inner>
                        )}
                    </MultiSearchSelect.S.Section>

                    <MultiSearchSelect.S.Section>
                        <MultiSearchSelect.S.Inner>
                            <MultiSearchSelect.Submit
                                text={'Submit'}
                                closeOnSubmit={false}
                            />
                            <MultiSearchSelect.Cancel
                                text={'Cancel'}
                                closeOnCancel={false}
                            />
                            <MultiSearchSelect.Reset
                                text={'Reset'}
                                closeOnReset={false}
                            />
                        </MultiSearchSelect.S.Inner>
                    </MultiSearchSelect.S.Section>
                </MultiSearchSelect.SearchLayout>
            </MultiSearchSelect>
        )}
    </WithState>
</>;
```

Основные статические компоненты: 

→ <b>SearchInput</b> — Поле поиска, отправляет запрос в апи при изменении.<br>Внутри использует <b>DebouncedInput</b>
```(jsx)
<>
    <MultiSearchSelect loadData={() => {}}>
        <MultiSearchSelect.SearchInput placeholder="Поиск" />
    </MultiSearchSelect>
</>
```

→ <b>List</b> — Выводит список <b>items</b><br>
→ <b>GroupList</b> — Выводит сгруппированные списки<br>

Внутри использует <b>SelectMenu.Item</b><br>
Позволяет переопределить вывода элементов списка через <b>renderItemLabel</b><br>
Для GroupList можно переопределить вывод названия группы через <b>renderGroupLabel</b><br>
<pre>
items = {
id: string | number;
label: string;
items: { // В случае вложенного списка
    id: string | number;
    label: string;
    }
}
</pre>

При переопределении рендера в каждый Item долонительно прокидывается его состояние
<pre>
    isSelected?: boolean;
    isPrevSelected?: boolean;
    isHighlighted?: boolean;
</pre>


```(jsx)
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
const renderItemLabel = ({label, isPrevSelected}) => {
    return <span>{label}</span>
}

<>
    <MultiSearchSelect loadData={() => {}} items={companyList}>
        <MultiSearchSelect.List renderItemLabel={renderItemLabel} />
    </MultiSearchSelect>
</>

```

→ Controls Button — <b>Submit, Cancel, Reset</b>.<br>
По дефолту закрывают попап, это поведение можно отменить, например <b>closeOnReset={false}</b><br>
Вызывают соотвествующие колбеки: 

<pre>
    onSubmit: (selectedItems: StateItem[]) => void; 
    onCancel: () => void;
    onReset: () => void; 
</pre>

→ <b>Total</b> — Позволяет через <b>renderTotal</b> вывести:
 - текущие количество элементов списка (total), 
 - количество выбранных элементов (totalSelected), 
 - количество выбранных элементов в стейте компонента (totalStateSelected), 

<pre>
    total: number;
    totalSelected: number;
    totalStateSelected: number;
</pre>
---
Стили:
   - S.Inner — ззадает дефолтные отступы внутри попапа
   - S.Section — для разделения попапа на секции


Компонент для выбора нескольких элементов из списка.
Основан на компоненте [TreeSelector](#treeselector), соответственно, принимает такие же пропсы.

Может быть как кнопкой, так и инпутом, примеры ниже.

Мультиселект
```jsx

const SelectedItemList = require('./SelectedItemList').default;
const SelectedItem = require('./SelectedItem').default;


const items = {
    a: 'Первый вариант',
    b: 'Второй вариант',
    c: 'Третий вариант',
    d: 'Четвёртый вариант',
};

const {initialState, onSelectionChange, onRemove} = ctx.MultiSelect({state, setState, selection: [], items});

<div>
    <MultiSelect
        onSelectionChange={onSelectionChange}
        selection={state.selection}
        rootId="root"
        items={state.items}
        placeholder={state.selection.length === 0 ? 'Выбери меня!' : `Выбрано ${state.selection.length}`}
    />

    <SelectedItemList onRemove={onRemove}>
        {state.selection.map(id => <SelectedItem id={id}>{items[id]}</SelectedItem>)}
    </SelectedItemList>
</div>
```

Мультиселект с поиском
```jsx
const SelectedItemList = require('./SelectedItemList').default;
const SelectedItem = require('./SelectedItem').default;

const items = {
    a: 'Первый вариант',
    b: 'Второй вариант',
    c: 'Третий вариант',
    d: 'Четвёртый вариант',
    e: 'Пятый вариант',
    f: 'Шестой вариант',
    g: 'Седьмой вариант',
    h: 'Восьмой вариант',
    i: 'Девятый вариант',
};

const {
    initialState,
    onSelectionChange,
    onSearchQueryChange,
    onRemove,
    onRemoveLast,
    onAppendByName,
} = ctx.MultiSelect({state, setState, selection: [], items});

<div>
    <MultiSelect
        onSelectionChange={onSelectionChange}
        onRemove={onRemove}
        selection={state.selection}
        rootId="root"
        items={state.items}
        placeholder="Введи текст"
        searchQuery={state.searchQuery}
        onSearchQueryChange={onSearchQueryChange}
        withSearch
    />

    <SelectedItemList onRemove={onRemove}>
        {state.selection.map(id => <SelectedItem id={id}>{items[id]}</SelectedItem>)}
    </SelectedItemList>
</div>
```

Мультиселект с поиском и возможностью удаления элементов по нажатиию Backspace и добавления по нажатиию Enter на инпуте
```jsx
const SelectedItemList = require('./SelectedItemList').default;
const SelectedItem = require('./SelectedItem').default;

const items = {
    a: 'Первый вариант',
    b: 'Второй вариант',
    c: 'Третий вариант',
    d: 'Четвёртый вариант',
    e: 'Пятый вариант',
    f: 'Шестой вариант',
    g: 'Седьмой вариант',
    h: 'Восьмой вариант',
    i: 'Девятый вариант',
};

const {
    initialState,
    onSelectionChange,
    onSearchQueryChange,
    onRemove,
    onRemoveLast,
    onAppendByName,
} = ctx.MultiSelect({state, setState, selection: [], items});

<MultiSelect
    onSelectionChange={onSelectionChange}
    onRemove={onRemove}
    selection={state.selection}
    rootId="root"
    items={state.items}
    placeholder="Введи текст для поиска"
    searchQuery={state.searchQuery}
    onSearchQueryChange={onSearchQueryChange}
    onRemoveLast={onRemoveLast}
    onAppendByName={onAppendByName}
    selectedItemList={
        <SelectedItemList onRemove={onRemove}>
            {state.selection.map(id => <SelectedItem id={id}>{items[id]}</SelectedItem>)}
        </SelectedItemList>
    }
    withSearch
/>
```

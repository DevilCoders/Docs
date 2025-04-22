Таблица

HOCS **used**: [withScrollShadow](#withscrollshadow)
HOCS **exported**: withTableData

```jsx
const arr = Array.from(Array(5));

const data = {
    titles: arr.map((_, i) => `Столбец ${i}`),
    values: arr.map((_, i) => arr.map((_, j) => `Значение ${i} ${j}`)),
};

<Table data={data} />
```

Длинная таблица с тенями при скролле:

```jsx
const arr1 = Array.from(Array(50));
const arr2 = Array.from(Array(5));

const data = {
    titles: arr1.map((_, i) => `Столбец ${i}`),
    values: arr2.map((_, i) => arr1.map((_, j) => `Значение ${i} ${j}`)),
};

<Table data={data} />
```

Таблица с уровнями вложенности:

HOCS **used**: withNesting

```jsx

const {default: Table, TableRows, TableRow, TableHead, TableBody, TableCell} = require('./');
const {withNesting} = require('./Body');
const TableBodyWithNesting = withNesting(TableBody);

const data = [
  {row: ['Level 0', 1, 2], nested: [
    {row: ['Level 1', 5, 6], nested: [
      {row: ['Level 2', 9, 10]},
      {row: ['Level 2', 11, 12]},
    ]},
    {row: ['Level 1', 15, 16]},
  ]},
  {row: ['Level 0', 3, 4], nested: [
    {row: ['Level 1', 5, 6]},
  ]},
];

<Table>
    <TableHead>
        <TableRow>{['Nesting level','foo','bar']}</TableRow>
    </TableHead>
    <TableBodyWithNesting data={data} />
</Table>

```

Таблица с группами:

HOCS **used**: withGroups

```jsx

const {default: Table, TableRows, TableRow, TableHead, TableBody, TableCell} = require('./');
const {withGroups} = require('./Body');
const TableBodyWithGroups = withGroups(TableBody);
const {contains, append, uniq, filter} = require('ramda');

expand = id => {
    expandedGroups = uniq(append(id, state.expandedGroups));
    setState(() => ({data: makeData(expandedGroups), expandedGroups}));
}
collapse = id => {
    expandedGroups = filter(groupId => groupId !== id, state.expandedGroups);
    setState(() => ({data: makeData(expandedGroups), expandedGroups}));
}

makeData = (expandedGroups = []) => {
    isExpanded = id => contains(id, expandedGroups);

    getGroupChildren = (id) => {
        switch(id) {
            case 1: return isExpanded(1) ? [
                {row: ['Утюги', 2], isGroup: true, id: 3, nested: getGroupChildren(3)},
                {row: ['Телевизоры', 2], isGroup: true, id: 4, nested: getGroupChildren(4)},
            ] : null;
            case 2: return isExpanded(2) ? [
                {row: ['Кровати', 2], isGroup: true, id: 5, nested: getGroupChildren(5)},
                {row: ['Стулья', 2], isGroup: true, id: 6, nested: getGroupChildren(6)},
            ] : null;
            case 3: return isExpanded(3) ? [
                {row: ['Мега-утюг 3000', 2]},
                {row: ['ИжМашУтюг "Железный дровосек"', 0]},
            ] : null;
            case 4: return isExpanded(4) ? [] : null;
            case 5: return isExpanded(5) ? [
                {row: ['Leather Сouch Delux', 1]},
                {row: ['СургутКожзамИзделие №12', 1]},
            ] : null;
            case 6: return isExpanded(6) ? [] : null;

        }
    }

    return [
        {row: [<b key={0}>Итого</b>, <b key={1}>10</b>]},
        {row: ['Электроника', 4], isGroup: true, id: 1, nested: getGroupChildren(1)},
        {row: ['Мебель', 4], isGroup: true, id: 2, nested: getGroupChildren(2)}
    ];
};

initialState = {data: makeData(), expandedGroups: []};

<Table>
    <TableHead>
        <TableRow>{['Товар/категория','Количество на складе']}</TableRow>
    </TableHead>
    <TableBodyWithGroups data={state.data} onExpand={expand} onCollapse={collapse} />
</Table>
```

С сортировкой:

```jsx
const {map, addIndex, sortBy, equals, nth, findIndex, compose, negate} = require('ramda');
const {default: Table, TableRow, TableBody, TableHead} = require('./');
const {withSorting} = require('./Row');
const TableRowWithSorting = withSorting(TableRow);

intitialState = {};

const columns = [
  {title: 'foo', sortKey: 'fooKey'},
  {title: 'bar'},
  {title: 'baz', sortKey: 'bazKey'},
];

const getSorted = () => {
  const unsorted = [
    [1, 2, 3],
    [4, 5, 6],
    [3, 2, 1],
  ];

  if (!state.key) return unsorted;

  let sortFn = nth(findIndex(equals(state.key), ['fooKey', 'barKey', 'bazKey']));
  if (state.order === 'asc') sortFn = compose(negate, sortFn);

  return sortBy(sortFn, unsorted);
}

const indexedMap = addIndex(map);

const makeRows = () => indexedMap(
  (values, index) => <TableRow key={index}>{[values]}</TableRow>,
  getSorted()
);

const setSorting = (key, order) => setState(() => ({key, order}));

<Table>
  <TableHead>
      <TableRowWithSorting
          columns={columns}
          sortedBy={state}
          onSort={setSorting}
      />
  </TableHead>
  <TableBody>
     {makeRows()}
  </TableBody>
</Table>
```

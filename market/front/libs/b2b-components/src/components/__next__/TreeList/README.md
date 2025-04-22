Абстрактное дерево-список с возможностью разворачивать (expand) и сворачивать (fold) узлы:

```js
const {default: TreeList} = require('.');
const {items, topItems} = require('./spec/mocks');
const state = {};
const onClick = ({expand, fold, id}) => {
    state[id] = !state[id];

    (state[id] ? expand : fold)(id);
};
const Item = ({children, depth, expand, fold, id, isExpanded, position}) => (
    <div
        onClick={() => onClick({expand, fold, id})}
        style={{margin: `8px ${40 * depth}px`, background: '#DDD', padding: '8px'}}
    >
        {position}
        {` ${id}, isExpanded: ${isExpanded}, children: ${children.length}`}
    </div>
);

<TreeList ItemComponent={Item} items={items} topItems={topItems} />
```

С живыми данными, общими и кастомными пропсами:
```js
const state = {};
const onClick = ({expand, fold, id}) => {
    state[id] = !state[id];

    (state[id] ? expand : fold)(id);
};
const Item = ({children, commonProp, customProp, depth, expand, fold, id, isExpanded, position}) => (
    <div
        onClick={() => onClick({expand, fold, id})}
        style={{margin: `8px ${40 * depth}px`, background: '#EEE', padding: '8px'}}
    >
        {position}
        {` ${id}, ${customProp || ''} ${commonProp || ''} `}
        {`isExpanded: ${isExpanded}, children: ${children.length}`}
    </div>
);

<TreeList
    ItemComponent={Item}
    itemComponentProps={{commonProp: 'Common!'}}
    items={[
        {id: 'foo'},
        {id: 'bar', children: ['quz']},
        {id: 'baz', customProp: 'Hi!'},
        {id: 'quz'},
    ]}
    topItems={['foo', 'bar', 'baz']}
/>
```
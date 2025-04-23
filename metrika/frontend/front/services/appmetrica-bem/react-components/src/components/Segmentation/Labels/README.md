Date filter label
```(jsx)
const { Tag } = require('@metrika/components');
const data = {
    from: new Date('2018-06-01'),
    to: new Date('2018-06-20'),
};
<Tag>
    <DateFilterLabel inverted={false} name="Установки" data={data} />
</Tag>
```

Tree filter label
```(jsx)
const { Tag } = require('@metrika/components');
const data = {
    values: [
        { tree: ['Россия', 'Московская обл.', 'г. Москва'] },
        { tree: ['Финляндия', 'Хельсинки'] },
    ]
};
<Tag>
    <TreeFilterLabel inverted={true} name="География" data={data} namesMap={{}} />
</Tag>
```

Multiselect filter label
```(jsx)
const { Tag } = require('@metrika/components');
const data = {
    values: [
        { value: 'Россия' },
        { value: 'Финляндия' },
    ]
};
<Tag>
    <MultiselectFilterLabel inverted={false} name="География" data={data} namesMap={{}} />
</Tag>
```

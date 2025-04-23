Табы без стейта

```jsx harmony
const {Tab, Tabs} = require('./index');

<Tabs value={state.value} onChange={value => setState({value})}>
    <Tab value={1}>Таб 1</Tab>
    <Tab value={2}>Таб 2</Tab>
    <Tab value={3}>Таб 3</Tab>
</Tabs>;
```

Сложный пример

```jsx harmony
const {Tab, TabRaw, Tabs} = require('./index');
const Select = require('../icon/Select').default;
const Settings = require('../icon/Settings').default;
const Button = require('../button').default;
const Dropdown = require('../dropdown').default;
const {List, Item, ItemCol, ItemContent} = require('../list');

const button1 = (
    <Button theme="none" size="m" iconEnd={<Select />}>
        Ещё
    </Button>
);

const button2 = <Button theme="none" size="m" icon={<Settings />} />;

const dropdown = (
    <Dropdown controlComponent={button1} placement="bottom">
        <List>
            <Item>
                <ItemCol>
                    <ItemContent title="Элемент списка 1" />
                </ItemCol>
            </Item>
            <Item>
                <ItemCol>
                    <ItemContent title="Элемент списка 2" />
                </ItemCol>
            </Item>
            <Item>
                <ItemCol>
                    <ItemContent title="Элемент списка 3" />
                </ItemCol>
            </Item>
            <Item>
                <ItemCol>
                    <ItemContent title="Элемент списка 4" />
                </ItemCol>
            </Item>
        </List>
    </Dropdown>
);

<Tabs value={state.value} onChange={value => setState({value})}>
    <Tab value={1}>Таб 1</Tab>
    <Tab value={2}>Таб 2</Tab>
    <Tab value={3}>Таб 3</Tab>
    <TabRaw size="">{dropdown}</TabRaw>
    <TabRaw size="">{button2}</TabRaw>
</Tabs>;
```

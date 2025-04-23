Древовидный список чекбоксов

```(jsx)
<TreeMultiselectLabel>Test</TreeMultiselectLabel>
```

```(jsx)
const MenuList = require('components/MenuList/MenuList').default;
const initialState = {loading: true};

<MenuList>
    <MenuList.Item>
        <TreeMultiselectLabel>
            Пункт 1
        </TreeMultiselectLabel>
    </MenuList.Item>
    <MenuList.Item>
        <TreeMultiselectLabel
            loading={state.loading}
            onCheckboxToggle={() => {setState({loading: !state.loading})}}
        >
            Пункт 2
        </TreeMultiselectLabel>
    </MenuList.Item>
    <MenuList.Item>
        <TreeMultiselectLabel
            collapsed={false}
        >
            Пункт 3
        </TreeMultiselectLabel>
    </MenuList.Item>
    <MenuList.Item
        level={1}
        padding={16}
    >
        <TreeMultiselectLabel>
            Пункт 3.1
        </TreeMultiselectLabel>
    </MenuList.Item>
    <MenuList.Item
        level={1}
        padding={16}
    >
        <TreeMultiselectLabel>
            Пункт 3.2
        </TreeMultiselectLabel>
    </MenuList.Item>
    <MenuList.Item
        level={1}
        padding={16}
    >
        <TreeMultiselectLabel>
            Пункт 3.3
        </TreeMultiselectLabel>
    </MenuList.Item>
</MenuList>
```

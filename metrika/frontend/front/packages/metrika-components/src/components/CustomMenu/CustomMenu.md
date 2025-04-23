Custom menu block with some features inside


```(jsx)
const { Search } = require('components');
initialState = {collapsed1: false, collapsed2: false};
<CustomMenu>
    <CustomMenu.SearchBlock>
        <Search />
    </CustomMenu.SearchBlock>
    <CustomMenu.Divider />
    <CustomMenu.Title>Заголовок</CustomMenu.Title>
    <CustomMenu.Divider />
    <CustomMenu.Item>Пункт</CustomMenu.Item>
    <CustomMenu.List>
        <CustomMenu.Item>
            <CustomMenu.Section
                collapsed={state.collapsed}
                onClick={() => {
                    console.log('Handle click on row. Toggle doesn\'t work in this case. Use toggler on the right side of row.');
                }}
                onToggle={() => setState(({collapsed}) => (
                    { collapsed: !collapsed }
                ))}
            >
                Секция
            </CustomMenu.Section>
        </CustomMenu.Item>
        {!state.collapsed &&
            <>
                <CustomMenu.Item level={1}>Пункт</CustomMenu.Item>
                <CustomMenu.Item level={1}>Пункт</CustomMenu.Item>
                <CustomMenu.Item level={1}>Пункт</CustomMenu.Item>
            </>
        }
    </CustomMenu.List>
    <CustomMenu.List>
            <CustomMenu.Item>
                <CustomMenu.Section
                    collapsed={state.collapsed2}
                    onToggle={() => setState(({collapsed2}) => (
                        { collapsed2: !collapsed2 }
                    ))}
                >
                    Секция
                </CustomMenu.Section>
            </CustomMenu.Item>
            {!state.collapsed2 &&
                <>
                    <CustomMenu.Item level={1}>Пункт</CustomMenu.Item>
                    <CustomMenu.Item level={1}>Пункт</CustomMenu.Item>
                    <CustomMenu.Item level={1}>Пункт</CustomMenu.Item>
                </>
            }
        </CustomMenu.List>
</CustomMenu>
```

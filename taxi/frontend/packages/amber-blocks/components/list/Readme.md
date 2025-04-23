Дефолтный список
```jsx harmony
const {Item, ItemCol, ItemContent} = require('./index');
const {LoremIpsum} = require('../../styleguide/components/lorem-ipsum');

<List>
    <Item>
        <ItemCol>
            <ItemContent title={<LoremIpsum n={20} />}/>
        </ItemCol>
    </Item>
    <Item onClick={() => {}}>
        <ItemCol>
            <ItemContent title="Интерактивный элемент списка"/>
        </ItemCol>
    </Item>
    <Item tabIndex={0} onKeyDown={() => {}}>
        <ItemCol>
            <ItemContent title="Интерактивный элемент списка"/>
        </ItemCol>
    </Item>
</List>
```

Список с заголовком
```jsx harmony
const Item = require('./Item').default;
const ItemCol = require('./ItemCol').default;
const ItemContent = require('./ItemContent').default;

<React.Fragment>
    <List title="Заголовок первого списка">
        <Item>
            <ItemCol>
                <ItemContent title="Элемент списка"/>
            </ItemCol>
        </Item>
        <Item>
            <ItemCol>
                <ItemContent title="Элемент списка"/>
            </ItemCol>
        </Item>
    </List>
    <List title="Заголовок второго списка">
        <Item>
            <ItemCol>
                <ItemContent title="Элемент списка"/>
            </ItemCol>
        </Item>
        <Item>
            <ItemCol>
                <ItemContent title="Элемент списка"/>
            </ItemCol>
        </Item>
        <Item header>
            <ItemCol>
                <ItemContent title="Но если очень хочеться, то можно и так"/>
            </ItemCol>
        </Item>
        <Item>
            <ItemCol>
                <ItemContent title="Элемент списка"/>
            </ItemCol>
        </Item>
    </List>
    <List title="Очень длинный заголовок. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.">
        <Item>
            <ItemCol>
                <ItemContent title="Элемент списка"/>
            </ItemCol>
        </Item>
    </List>
</React.Fragment>
```

Список с контролами
```jsx harmony
const Tumbler = require('../tumbler/Tumbler').default;
const WalletIcon = require('../icon/Wallet').default;
const Checkbox = require('../checkbox/Checkbox').default;
const Radio = require('../radio/Radio').default;
const Item = require('./Item').default;
const ItemCol = require('./ItemCol').default;
const ItemContent = require('./ItemContent').default;

const onChange = () => {};

<List title="Контролы">
    <Item>
        <ItemCol grow>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
        <ItemCol>
            <Tumbler/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <WalletIcon/>
        </ItemCol>
        <ItemCol grow>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
        <ItemCol>
            <Tumbler onChange={onChange} label='label'/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <Checkbox onChange={onChange} checked label="label"/>
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <Checkbox onChange={onChange} />
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol grow>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
        <ItemCol>
            <Checkbox onChange={onChange} checked/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <Radio onChange={onChange} checked/>
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка с радио кнопкой"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <Radio onChange={onChange}/>
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка с радио кнопкой"/>
        </ItemCol>
    </Item>
</List>
```

Список с иконками
```jsx harmony
const SettingsIcon = require('../icon/Settings').default;
const WalletIcon = require('../icon/Wallet').default;
const CameraIcon = require('../icon/Camera').default;
const Item = require('./Item').default;
const ItemCol = require('./ItemCol').default;
const ItemContent = require('./ItemContent').default;

<List title="Значки">
    <Item>
        <ItemCol>
            <SettingsIcon fill="green"/>
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <WalletIcon fill="grey"/>
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <CameraIcon fill="red"/>
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <SettingsIcon fill="green"/>
        </ItemCol>
        <ItemCol>
            <WalletIcon fill="grey"/>
        </ItemCol>
        <ItemCol>
            <CameraIcon fill="red"/>
        </ItemCol>
        <ItemCol>
            <ItemContent title="Элемент списка"/>            
        </ItemCol>
    </Item>
    <Item>
        <ItemCol>
            <SettingsIcon fill="green"/>
        </ItemCol>
        <ItemCol grow>
            <ItemContent title="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."/>
        </ItemCol>
        <ItemCol>
            <WalletIcon fill="grey"/>
        </ItemCol>
        <ItemCol>
            <CameraIcon fill="red"/>
        </ItemCol>
    </Item>
</List>
```

Список с пояснением
```jsx harmony
const Item = require('./Item').default;
const SettingsIcon = require('../icon/Settings').default;
const ItemCol = require('./ItemCol').default;
const ItemColChevron = require('./ItemColChevron').default;
const ItemContent = require('./ItemContent').default;

<List title="Заголовок">
    <Item>
        <ItemColChevron>
            <ItemContent title="Элемент списка" description="Пояснение"/>
        </ItemColChevron>
    </Item>
    <Item>
        <ItemColChevron>
            <ItemContent 
                title="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum." 
                description="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
            />
        </ItemColChevron>
    </Item>
    <Item>
        <ItemCol>
            <SettingsIcon/>
        </ItemCol>
        <ItemColChevron>
            <ItemContent title="Элемент списка с иконкой" description="Пояснение"/>
        </ItemColChevron>
    </Item>
    <Item>
        <ItemColChevron>
            <ItemContent title="Элемент списка"/>
        </ItemColChevron>
    </Item>
</List>
```

Список в выбором  
```jsx harmony
const Item = require('./Item').default;
const ItemCol = require('./ItemCol').default;
const ItemColCheck = require('./ItemColCheck').default;
const ItemContent = require('./ItemContent').default;
const SettingsIcon = require('../icon/Settings').default;

<List title="Заголовок">
    <Item>
        <ItemColCheck checked>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
    </Item>
    <Item>
        <ItemColCheck>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
    </Item>
    <Item header>
        <ItemCol>
            <ItemContent title="Можно даже так"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemColCheck checked>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
        <ItemCol>
            <SettingsIcon fill="grey"/>
        </ItemCol>
    </Item>
    <Item>
        <ItemColCheck>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
        <ItemCol>
            <SettingsIcon fill="grey"/>
        </ItemCol>
    </Item>
</List>
```

Список с disabled 
```jsx harmony
const Item = require('./Item').default;
const ItemCol = require('./ItemCol').default;
const ItemColCheck = require('./ItemColCheck').default;
const ItemContent = require('./ItemContent').default;
const SettingsIcon = require('../icon/Settings').default;

<List title="Заголовок">
    <Item disabled>
        <ItemColCheck checked>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
    </Item>
    <Item disabled>
        <ItemColCheck>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
    </Item>
    <Item header>
        <ItemCol>
            <ItemContent title="Можно даже так"/>
        </ItemCol>
    </Item>
    <Item disabled>
        <ItemColCheck checked>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
        <ItemCol>
            <SettingsIcon fill="grey"/>
        </ItemCol>
    </Item>
    <Item disabled>
        <ItemColCheck>
            <ItemContent title="Элемент списка"/>
        </ItemColCheck>
        <ItemCol>
            <SettingsIcon fill="grey"/>
        </ItemCol>
    </Item>
</List>
```

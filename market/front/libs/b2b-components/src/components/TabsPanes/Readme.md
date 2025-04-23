Табы с радио-кнопкой
```jsx

const withRadioGroup = require('./Tabs/withRadioGroup').default;
const Tabs = withRadioGroup(require('./Tabs').default);
const Pane = require('./Pane').default;
const RadioGroup = require('../RadioGroup').default;
const Button = require('../RadioGroup/Items/Button').default;

const tabsPanes = ctx.TabsPanes({state, setState, checked: 1});

const {initialState, onTabChange} = tabsPanes;

<TabsPanes onTabChange={onTabChange} checked={state.checked}>
    <Tabs>
        <RadioGroup>
            <Button value={1}>Tab 1</Button>
            <Button value={2}>Tab 2</Button>
        </RadioGroup>
    </Tabs>
    <Pane id={1}>Pane 1</Pane>
    <Pane id={2}>Pane 2</Pane>
</TabsPanes>
```

Табы с кастомными переключателями
```jsx

const Tabs = require('./Tabs').default;
const Pane = require('./Pane').default;
const RadioGroup = require('../RadioGroup').default;
const Button = require('../RadioGroup/Items/Button').default;

const tabsPanes = ctx.TabsPanes({state, setState, checked: 1});

const {initialState, onTabChange} = tabsPanes;

const defaultStyles = {cursor: 'pointer', merginRight: 10, padding: 10, display: 'inline-block', marginBottom: 10};
const selectedStyles = {...defaultStyles, borderBottom: '2px solid red'};

const CustomTab = ({children, value, checked, ...props}) => (
    <div style={checked ? selectedStyles : defaultStyles} data-value={value} {...props}>
        {children}
    </div>
);

const CustomTabs = ({onTabChange, onChange, children, checked}) => (
    <div>
        {React.Children.map(children, (child, i) => (
            React.cloneElement(child, {
                key: i,
                checked: checked === child.props.value,
                onClick: event => {
                    if (onTabChange) onTabChange(child.props.value);
                    if (onChange) onChange(event);
                },
            })
        ))}
    </div>
);

<TabsPanes onTabChange={onTabChange} checked={state.checked}>
    <Tabs>
        <CustomTabs>
            <CustomTab value={1}>Tab 1</CustomTab>
            <CustomTab value={2}>Tab 2</CustomTab>
        </CustomTabs>
    </Tabs>
    <Pane id={1}>Pane 1</Pane>
    <Pane id={2}>Pane 2</Pane>
</TabsPanes>
```

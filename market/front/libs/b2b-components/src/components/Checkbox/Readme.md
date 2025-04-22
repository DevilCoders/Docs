Чекбокс
```jsx
initialState = {checked: true};
const toggle = () => setState(({checked}) => ({checked: !checked}));

const liStyle = {
    display: 'flex',
    margin: '5px 0'
};

<div>
    <div style={{paddingBottom: '5px'}}>Обычный чекбокс:</div>
    <ul>
        <li style={liStyle}>
            <div style={{paddingRight: 10}}>Обычный:</div>
            <Checkbox
                checked={state.checked}
                disabled={false}
                onChange={toggle}
            />
        </li>
        <li style={liStyle}>
            <div style={{paddingRight: 10}}>disabled:</div>
            <Checkbox
                checked={state.checked}
                disabled={true}
                onChange={toggle}
            />
        </li>
        <li style={liStyle}>
            <div style={{paddingRight: 10}}>Частично выбранный:</div>
            <Checkbox
                indeterminate={true}
                disabled={false}
                onChange={toggle}
            />
        </li>
    </ul>
    <br/>
    <div style={{paddingBottom: '5px'}}>Чекбокс с theme: white</div>
    <ul>
        <li style={liStyle}>
            <div style={{paddingRight: 10}}>Обычный:</div>
            <Checkbox
                theme="white"
                checked={state.checked}
                disabled={false}
                onChange={toggle}
            />
        </li>
        <li style={liStyle}>
            <div style={{paddingRight: 10}}>disabled:</div>
            <Checkbox
                theme="white"
                checked={state.checked}
                disabled={true}
                onChange={toggle}
            />
        </li>
        <li style={liStyle}>
            <div style={{paddingRight: 10}}>Частично выбранный:</div>
            <Checkbox
                theme="white"
                indeterminate={true}
                disabled={false}
                onChange={toggle}
            />
        </li>
    </ul>
</div>
```
handleDisabled срабатывает при клике в задизейбленный чекбокс

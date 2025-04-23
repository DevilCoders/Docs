Radio

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const {generate} = require('../../styleguide/components/lorem-ipsum/LoremIpsum');

items = [
    {label: 'label1', value: 1}, 
    {label: 'label2', value: 2}, 
    {label: generate(20), value: 3},
    {label: 'label3', value: 4, disabled: true},
];

initialState = {value: items[1].value};

<Grid container spacing={2} style={{width: 600}}>
    <Grid item spacing={2} size={6}>
        <h3>view_dot</h3>
        {items.map((item, index) => (
            <div key={index} style={{marginBottom: 10}}>
                <Radio
                    onChange={value => {
                        setState({value: value});
                    }}
                    name="radio1"
                    value={item.value}
                    label={item.label}
                    disabled={item.disabled}
                    checked={state.value === item.value}
                />
            </div>
        ))}
    </Grid>
    <Grid item spacing={2} size={6}>
        <h3>view_tick</h3>
        {items.map((item, index) => (
            <div key={index} style={{marginBottom: 10}}>
                <Radio
                    onChange={value => {
                        setState({value: value});
                    }}
                    name="radio1"
                    view="tick"
                    value={item.value}
                    label={item.label}
                    disabled={item.disabled}
                    checked={state.value === item.value}
                />
            </div>
        ))}
    </Grid>
    <Grid item spacing={2} size={6}>
        <h3>С ошибкой view_dot</h3>
        {items.map((item, index) => (
            <div key={index} style={{marginBottom: 10}}>
                <Radio
                    onChange={value => {
                        setState({value: value});
                    }}
                    name="radio1"
                    value={item.value}
                    label={item.label}
                    error
                    disabled={item.disabled}
                    checked={state.value === item.value}
                />
            </div>
        ))}
    </Grid>
    <Grid item spacing={2} size={6}>
        <h3>С ошибкой view_tick</h3>
        {items.map((item, index) => (
            <div key={index} style={{marginBottom: 10}}>
                <Radio
                    onChange={value => {
                        setState({value: value});
                    }}
                    name="radio1"
                    value={item.value}
                    label={item.label}
                    error
                    view="tick"
                    disabled={item.disabled}
                    checked={state.value === item.value}
                />
            </div>
        ))}
    </Grid>
</Grid>;
```

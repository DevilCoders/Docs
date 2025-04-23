```jsx harmony
initialState = {value: 20};

const Grid = require('../../styleguide/components/grid/Grid').default;
<Grid container spacing={2} style={{width: 600}}>
    <Grid item spacing={2} size={6}>
        M
    </Grid>
    <Grid item spacing={2} size={6}>
        L
    </Grid>
    <Grid item spacing={2} size={6}>
        <InputRange
            size="m"
            value={state.value}
            min={10}
            max={50}
            labels={[
                {value: 10, label: '10'},
                {value: 20, label: '20'},
                {value: 30, label: '30'},
                {value: 40, label: '40'},
                {value: 50, label: '50'}
            ]}
            onChange={e => {
                setState({value: e.target.value});
            }}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <InputRange
            size="l"
            value={state.value}
            min={10}
            max={50}
            labels={[
                {value: 10, label: '10'},
                {value: 20, label: '20'},
                {value: 30, label: '30'},
                {value: 40, label: '40'},
                {value: 50, label: '50'}
            ]}
            onChange={e => {
                setState({value: e.target.value});
            }}
        />
    </Grid>
</Grid>
```

**Произвольные labels**
```jsx harmony
const Button = require('../button').default;

initialState = {value: 20};
<div>
<InputRange
    size="l"
    value={state.value}
    min={10}
    max={50}
    labels={[
        {value: 10, label: '10'},
        {value: 30, label: '30'},
        {value: 50, label: '50'}
    ]}
    renderLabel={(value, label) => {
        return (<Button onClick={() => {setState({value: label.value})}}>{Number(value) - label.value}</Button>)
    }}
    onChange={e => {
        setState({value: e.target.value});
    }}
/>

<InputRange
    size="l"
    value={state.value}
    min={10}
    max={50}
    labels={[
        {value: 10, label: '10'},
        {value: 30, label: <a href="#">30</a>},
        {value: 50, label: '50'}
    ]}
    onChange={e => {
        setState({value: e.target.value});
    }}
/>
</div>
```

**Error**
```jsx harmony
<InputRange
    size="m"
    value={state.value}
    min={10}
    max={50}
    error
    labels={[
        {value: 10, label: '10'},
        {value: 20, label: '20'},
        {value: 30, label: '30'},
        {value: 40, label: '40'},
        {value: 50, label: '50'}
    ]}
    onChange={e => {
        setState({value: e.target.value});
    }}
/>

```
**Disabled**
```jsx harmony
<InputRange
    size="m"
    value={state.value}
    min={10}
    max={50}
    disabled
    labels={[
        {value: 10, label: '10'},
        {value: 20, label: '20'},
        {value: 30, label: '30'},
        {value: 40, label: '40'},
        {value: 50, label: '50'}
    ]}
    onChange={e => {
        setState({value: e.target.value});
    }}
/>
```

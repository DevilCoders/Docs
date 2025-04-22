```js

const initialState = { isChecked: false };
const onChange = () => {
    setState({
        isChecked: !state.isChecked,
    });
};

<div style={{width: '300px'}}>
    <FilterTumbler
        name="name"
        type="switch"
        isChecked={state.isChecked}
        onCheck={onChange}
        onUncheck={onChange}
    />
</div>
```


```js

const initialState = { isChecked: false };
const onChange = () => {
    setState({
        isChecked: !state.isChecked,
    });
};

<div style={{width: '300px'}}>
    <FilterTumbler
        name="name"
        type="checkbox"
        isChecked={state.isChecked}
        onCheck={onChange}
        onUncheck={onChange}
    />
</div>
```

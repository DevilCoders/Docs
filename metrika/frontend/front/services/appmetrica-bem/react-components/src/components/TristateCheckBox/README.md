Чекбокс с тремя состояниями

```(jsx)
initialState={checked: 'no'};

<div style={{
    display: 'flex',
    justifyContent: 'space-between',
}}
>
    <TristateCheckBox
        checked="indeterminate"
        theme="normal"
        size="s"
        onChange={() => {console.log('change')}}
    >
        checked indeterminate, size s
    </TristateCheckBox>

    <TristateCheckBox
        checked={state.checked}
        theme="normal"
        size="s"
        onChange={() => setState({ checked: (state.checked === 'yes') ? 'no' : 'yes' })}
    >
        interactive, size s
    </TristateCheckBox>

    <TristateCheckBox
        checked="indeterminate"
        theme="normal"
        size="m"
        disabled={true}
        onChange={() => {console.log('change')}}
    >
        checked indeterminate, size m
    </TristateCheckBox>

    <TristateCheckBox
        checked="indeterminate"
        theme="normal"
        size="n"
    >
        checked indeterminate, size n
    </TristateCheckBox>

    <TristateCheckBox
        checked="yes"
        theme="normal"
        size="n"
    >
        checked yes
    </TristateCheckBox>
</div>
```

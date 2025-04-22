Как легошный чекбокс, только цветной

```(jsx)
const { ControlsList } = require('components');
const { WithState } = require('utils/WithState');

<ControlsList>
    <WithState state={{ checked: true }}>
        {(state, updateState) => (
            <ColorCheckBox
                size="s"
                color="blue"
                theme="normal"
                checked={state.checked}
                onChange={() => updateState({ checked: !state.checked })}
            >Size S</ColorCheckBox>
        )}
    </WithState>
    <WithState state={{ checked: true }}>
        {(state, updateState) => (
            <ColorCheckBox
                size="m"
                color="green"
                theme="normal"
                checked={state.checked}
                onChange={() => updateState({ checked: !state.checked })}
            >Size M</ColorCheckBox>
        )}
    </WithState>
    <WithState state={{ checked: true }}>
        {(state, updateState) => (
            <ColorCheckBox
                size="n"
                color="red"
                theme="normal"
                checked={state.checked}
                onChange={() => updateState({ checked: !state.checked })}
            >Size N</ColorCheckBox>
        )}
    </WithState>
    <WithState state={{ checked: false }}>
        {(state, updateState) => (
            <ColorCheckBox
                size="n"
                color="red"
                theme="normal"
                checked={state.checked}
                indeterminate={true}
                onChange={() => updateState({ checked: !state.checked })}
            >Size N</ColorCheckBox>
        )}
    </WithState>
</ControlsList>
```

С индикацией удаления, для легенды
```(jsx)
const { ControlsList } = require('components');
const { WithState } = require('utils/WithState');

<ControlsList>
    <WithState state={{ checked: true }}>
        {(state, updateState) => (
            <ColorCheckBox
                size="s"
                color="magenta"
                theme="normal"
                cancelable
                checked={state.checked}
                onChange={() => updateState({ checked: !state.checked })}
            >Удали меня</ColorCheckBox>
        )}
    </WithState>
</ControlsList>
```
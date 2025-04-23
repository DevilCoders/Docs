 Комонент визард.
```(jsx)
const { WithState } = require('utils/WithState');
<>
    <WithState state={{ step: 1 }}>
        {(state, updateState) => (
            <StepIndicator
                current={state.step}
                onSelectStep={(index) => updateState({ step: index })}
                children={['step 1', 'step 2', 'step 2']}
             />
        )}
    </WithState>
</>;
```

Раскрывашка

```(jsx)
const { WithState } = require('utils/WithState');
const nextStateMap = {
    closed: 'opened',
    opened: 'closed',
};
const nextStateLoadingMap = {
    closed: 'loading',
    loading: 'opened',
    opened: 'closed',
};

const componentCallback = (state, setState) => {
    return (
        <PlusExpander size="m" state={state.state} onClick={(incomingState) => {
            const nextState = state.nextStateMap[incomingState];

            if (nextState) {
                setState({ state: nextState });
            }
        }} />
    );
};

<>
    Можно кликать:
    <br />
    <br />
    <WithState state={{ state: 'closed', nextStateMap: nextStateLoadingMap }}>
        {componentCallback}
    </WithState>
    <br />
    <br />
    <WithState state={{ state: 'closed', nextStateMap }}>
        {componentCallback}
    </WithState>
</>
```

Размеры
```(jsx)
<>
S — <PlusExpander size="s" state="opened" /> | <PlusExpander size="s" state="closed" /> | <PlusExpander size="s" state="loading" />
<br /><br />
M — <PlusExpander size="m" state="opened" /> | <PlusExpander size="m" state="closed" /> | <PlusExpander size="m" state="loading" />
</>
```

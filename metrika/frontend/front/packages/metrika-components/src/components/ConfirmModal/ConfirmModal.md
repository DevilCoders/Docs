Простая модалка с выбором ответа из двух вариантов

```(jsx)
const { Button } = require('lego');

initialState = {
    visible: false,
    chosen: null,
};
<div>
    <Button
        onClick={() => setState({visible: true})}
        theme="normal"
        size="s"
    >
        Open
    </Button> <span>Result: {state.chosen}</span>
    <ConfirmModal
        title="Hello"
        visible={state.visible}
        body="Here goes the content"
        yesLabel="OK"
        noLabel="Not OK"
        onYes={() => setState({visible: false, chosen: 'yes'})}
        onNo={() => setState({visible: false, chosen: 'no'})}
    />
</div>
```

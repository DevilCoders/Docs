```jsx
const radiobox = ctx.Radiobox({state, setState, checked: '0.53'});

const {initialState, onChange} = radiobox;

<Container>
    <Label text="Дефолтная тема">
        <div style={{marginBottom: '15px'}}>
            <Radiobox
                name='testBox'
                onChange={onChange}
                buttons={
                    ['0', '0.17', '0.32', '0.53', '0.75', '1']
                        .map(value => ({
                            label: `${value}`,
                            value,
                            checked: radiobox.value === value,
                        }))
                    }
            />
        </div>
        <ProgressBar value={radiobox.value} />
    </Label>
</Container>
```

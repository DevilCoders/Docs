В состоянии "свернуто" показывает иконку "+", в состоянии развернуто показывает иконку "-".

```(jsx)
initialState={expanded: false};

<div style={{
    display: 'flex',
    justifyContent: 'space-between',
    maxWidth: '25%'
}}
>
    <ToggleExpander
        expanded={false}
        onClick={() => {console.log('clicked')}}
    />

    <ToggleExpander
        expanded={true}
        onClick={() => {console.log('clicked')}}
    />

    <ToggleExpander
        expanded={state.expanded}
        onClick={() => {setState({
                expanded: !state.expanded
            })}
        }
    />
</div>
```

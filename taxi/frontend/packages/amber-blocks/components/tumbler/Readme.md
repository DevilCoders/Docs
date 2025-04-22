```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
<Grid container spacing={2}>
    <Grid item spacing={2} size={6}>
        size M
    </Grid>
    <Grid item spacing={2} size={6}>
        size L
    </Grid>
    <Grid item spacing={2} size={6}>
        <Tumbler
            label="Жми меня"
            checked={state.checked || false}
            onChange={() => setState({ checked: !state.checked })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Tumbler
            size="l"
            label="Жми меня"
            checked={state.checked || false}
            onChange={() => setState({ checked: !state.checked })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Tumbler
            disabled
            label="Жми меня"
            checked={state.checked || false}
            onChange={() => setState({ checked: !state.checked })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Tumbler
            size="l"
            disabled
            label="Жми меня"
            checked={state.checked || false}
            onChange={() => setState({ checked: !state.checked })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Tumbler
            checked={state.checked || false}
            onChange={() => setState({ checked: !state.checked })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Tumbler
            size="l"
            checked={state.checked || false}
            onChange={() => setState({ checked: !state.checked })}
        />
    </Grid>
</Grid>

```

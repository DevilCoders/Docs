Кнопка-span

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const ButtonGroup = require('../button-group').default;

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <ButtonSpan theme="fill" size="m">
                Кнопка
            </ButtonSpan>
            <ButtonSpan theme="outline" size="m">
                Кнопка
            </ButtonSpan>
            <ButtonSpan theme="accent" size="m">
                Кнопка
            </ButtonSpan>
            <ButtonSpan theme="color" size="m">
                Кнопка
            </ButtonSpan>
            <ButtonSpan disabled>
                Кнопка
            </ButtonSpan>
        </ButtonGroup>
    </Grid>
</Grid>;
```

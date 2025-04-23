Компонент загрузки контента

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;

<Grid container spacing={2}>
    <Spinner style={{animation: 'none'}}/>
</Grid>;
```

Размеры

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;

<Grid container spacing={2}>
    {['xs', 's', 'm', 'l', 'xl', 'xxl'].map(size => (
        <Grid item key={size} spacing={2} size={2}>
            <Spinner size={size} style={{animation: 'none'}}/>
        </Grid>
    ))}
</Grid>;
```

Цвет

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;

<Grid container spacing={2}>
    <Spinner color="#fa3e2c" style={{animation: 'none'}}/>
</Grid>;
```

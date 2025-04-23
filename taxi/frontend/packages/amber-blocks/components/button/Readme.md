Кнопка

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const ButtonGroup = require('../button-group').default;

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="s">
                Нажать
            </Button>
            <Button theme="outline" size="s">
                Нажать
            </Button>
            <Button theme="accent" size="s">
                Нажать
            </Button>
            <Button theme="color" size="s">
                Нажать
            </Button>
            <Button theme="go" size="s">
                Нажать
            </Button>
            <Button isRound theme="go-accent" size="s">
                Нажать
            </Button>
            <Button theme="go-outline" size="s">
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="m">
                Нажать
            </Button>
            <Button theme="outline" size="m">
                Нажать
            </Button>
            <Button theme="accent" size="m">
                Нажать
            </Button>
            <Button theme="color" size="m">
                Нажать
            </Button>
            <Button theme="go" size="m">
                Нажать
            </Button>
            <Button isRound theme="go-accent" size="m">
                Нажать
            </Button>
            <Button theme="go-outline" size="m">
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="l">
                Нажать
            </Button>
            <Button theme="outline" size="l">
                Нажать
            </Button>
            <Button theme="accent" size="l">
                Нажать
            </Button>
            <Button theme="color" size="l">
                Нажать
            </Button>
            <Button theme="go" size="l">
                Нажать
            </Button>
            <Button isRound theme="go-accent" size="l">
                Нажать
            </Button>
            <Button theme="go-outline" size="l">
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="xl">
                Нажать
            </Button>
            <Button theme="outline" size="xl">
                Нажать
            </Button>
            <Button theme="accent" size="xl">
                Нажать
            </Button>
            <Button theme="color" size="xl">
                Нажать
            </Button>
            <Button theme="go" size="xl">
                Нажать
            </Button>
            <Button isRound theme="go-accent" size="xl">
                Нажать
            </Button>
            <Button theme="go-outline" size="xl">
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
</Grid>;
```

Кнопка с иконкой

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const Location = require('../icon/Location').default;
const Select = require('../icon/Select').default;
const ButtonGroup = require('../button-group').default;

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="s" iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="s" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="s" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="s" icon={<Location/>}/>
            <Button theme="go" size="s" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-accent" size="s" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-outline" size="s" icon={<Location/>}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="m" iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="m" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="m" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="m" icon={<Location/>}/>
            <Button theme="go" size="m" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-accent" size="m" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-outline" size="m" icon={<Location/>}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="l" iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="l" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="l" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="l" icon={<Location/>}/>
            <Button theme="go" size="l" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-accent" size="l" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-outline" size="l" icon={<Location/>}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="xl" iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="xl" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="xl" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="xl" icon={<Location/>}/>
            <Button theme="go" size="xl" iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-accent" size="xl" iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="go-outline" size="xl" icon={<Location/>}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
</Grid>;
```

Фиксированная ширина

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const Location = require('../icon/Location').default;
const Select = require('../icon/Select').default;
const ButtonGroup = require('../button-group').default;

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="s" iconStart={<Location />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="outline" size="s" iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="accent" size="s" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="go" size="s" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="m" iconStart={<Location />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="outline" size="m" iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="accent" size="m" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="go" size="m" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="l" iconStart={<Location />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="outline" size="l" iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="accent" size="l" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="go" size="l" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="xl" iconStart={<Location />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="outline" size="xl" iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="accent" size="xl" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
            <Button theme="go" size="xl" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Нажать
            </Button>
        </ButtonGroup>
    </Grid>
<Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="xl" iconStart={<Location />} style={{width: 200}}>
                Длинный длинный текст
            </Button>
            <Button theme="outline" size="xl" iconEnd={<Select />} style={{width: 200}}>
                Длинный длинный текст
            </Button>
            <Button theme="accent" size="xl" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Длинный длинный текст
            </Button>
            <Button theme="go" size="xl" iconStart={<Location />} iconEnd={<Select />} style={{width: 200}}>
                Длинный длинный текст
            </Button>
        </ButtonGroup>
    </Grid>
</Grid>;
```

Кнопка с onClick

```jsx harmony
const ButtonGroup = require('../button-group').default;

<ButtonGroup>
    <Button theme="accent" onClick={() => alert('Кнопка нажата!')}>
        Нажми меня
    </Button>
    <Button disabled theme="accent" onClick={() => alert('Кнопка нажата!')}>
        Кнопка отключена
    </Button>
</ButtonGroup>
```

Кнопка с disabled

```jsx harmony
const ButtonGroup = require('../button-group').default;

<ButtonGroup>
    <Button theme="fill" disabled>
        Нажать
    </Button>
    <Button theme="outline" disabled>
        Нажать
    </Button>
    <Button theme="accent" disabled>
        Нажать
    </Button>
    <Button theme="color" disabled>
        Нажать
    </Button>
    <Button theme="go" disabled>
        Нажать
    </Button>
    <Button theme="go-accent" disabled>
        Нажать
    </Button>
</ButtonGroup>
```

Загрузка

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const Location = require('../icon/Location').default;
const Select = require('../icon/Select').default;
const ButtonGroup = require('../button-group').default;

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="s" loading iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="s" loading iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="s" loading iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="s" loading icon={<Location/>}/>
            <Button theme="go" size="s" loading icon={<Location/>}/>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="m" loading iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="m" loading iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="m" loading iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="m" loading icon={<Location/>}/>
            <Button theme="go" size="m" loading icon={<Location/>}/>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="l" loading iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="l" loading iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="l" loading iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="l" loading icon={<Location/>}/>
            <Button theme="go" size="l" loading icon={<Location/>}/>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <Button theme="fill" size="xl" loading iconStart={<Location />}>
                Нажать
            </Button>
            <Button theme="outline" size="xl" loading iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="accent" size="xl" loading iconStart={<Location />} iconEnd={<Select />}>
                Нажать
            </Button>
            <Button theme="color" size="xl" loading icon={<Location/>}/>
            <Button theme="go" size="xl" loading icon={<Location/>}/>
        </ButtonGroup>
    </Grid>
</Grid>;
```

Тултип

```jsx harmony
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Grid = require('../../styleguide/components/grid/Grid').default;
const {PLACEMENTS} = require('./examples/consts');
const Button = require('../button').default;

const getTooltip = placement => (
    <div style={{padding: 8}}>
        <Tooltip open placement={placement} content={<LoremIpsum n={3} />}>
            <Button>{`Расположение ${placement}`}</Button>
        </Tooltip>
    </div>
);

<div style={{width: 500}}>
    <Grid container justify="center">
        <Grid item>{getTooltip('top')}</Grid>
    </Grid>
    <Grid container justify="center">
        <Grid container item size={6} direction="column">
            <Grid item>{getTooltip('left')}</Grid>
        </Grid>
        <Grid container item size={6} direction="column" alignItems="flex-end">
            <Grid item>{getTooltip('right')}</Grid>
        </Grid>
    </Grid>
    <Grid container justify="center">
        <Grid item>{getTooltip('bottom')}</Grid>
    </Grid>
</div>;
```

Разные расположения

```jsx harmony
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Grid = require('../../styleguide/components/grid/Grid').default;
const {PLACEMENTS} = require('./examples/consts');
const Button = require('../button').default;

const getTooltip = placement => (
    <div style={{padding: 8}}>
        <Tooltip enableClickListener placement={placement} content={<LoremIpsum n={3} />}>
            <Button>{`Расположение ${placement}`}</Button>
        </Tooltip>
    </div>
);

<div style={{width: 800}}>
    <Grid container justify="center">
        <Grid item>{getTooltip('top-start')}</Grid>
        <Grid item>{getTooltip('top')}</Grid>
        <Grid item>{getTooltip('top-end')}</Grid>
    </Grid>
    <Grid container justify="center">
        <Grid container item size={6} direction="column">
            <Grid item>{getTooltip('left-start')}</Grid>
            <Grid item>{getTooltip('left')}</Grid>
            <Grid item>{getTooltip('left-end')}</Grid>
        </Grid>
        <Grid container item size={6} direction="column" alignItems="flex-end">
            <Grid item>{getTooltip('right-start')}</Grid>
            <Grid item>{getTooltip('right')}</Grid>
            <Grid item>{getTooltip('right-end')}</Grid>
        </Grid>
    </Grid>
    <Grid container justify="center">
        <Grid item>{getTooltip('bottom-start')}</Grid>
        <Grid item>{getTooltip('bottom')}</Grid>
        <Grid item>{getTooltip('bottom-end')}</Grid>
    </Grid>
</div>;
```

Много контента

```jsx harmony
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Grid = require('../../styleguide/components/grid/Grid').default;
const {PLACEMENTS} = require('./examples/consts');
const Button = require('../button').default;

const getTooltip = placement => (
    <div style={{padding: 8}}>
        <Tooltip
            enableClickListener
            placement={placement}
            content={
                <div>
                    <div>
                        <LoremIpsum n={3} />
                    </div>
                    <div>
                        <LoremIpsum n={4} />
                    </div>
                    <div>
                        <LoremIpsum n={5} />
                    </div>
                    <div>
                        <LoremIpsum n={2} />
                    </div>
                    <div>
                        <LoremIpsum n={5} />
                    </div>
                </div>
            }
        >
            <Button>{`Расположение ${placement}`}</Button>
        </Tooltip>
    </div>
);

<div style={{width: 800}}>
    <Grid container justify="center">
        <Grid item>{getTooltip('top-start')}</Grid>
        <Grid item>{getTooltip('top')}</Grid>
        <Grid item>{getTooltip('top-end')}</Grid>
    </Grid>
    <Grid container justify="center">
        <Grid container item size={6} direction="column">
            <Grid item>{getTooltip('left-start')}</Grid>
            <Grid item>{getTooltip('left')}</Grid>
            <Grid item>{getTooltip('left-end')}</Grid>
        </Grid>
        <Grid container item size={6} direction="column" alignItems="flex-end">
            <Grid item>{getTooltip('right-start')}</Grid>
            <Grid item>{getTooltip('right')}</Grid>
            <Grid item>{getTooltip('right-end')}</Grid>
        </Grid>
    </Grid>
    <Grid container justify="center">
        <Grid item>{getTooltip('bottom-start')}</Grid>
        <Grid item>{getTooltip('bottom')}</Grid>
        <Grid item>{getTooltip('bottom-end')}</Grid>
    </Grid>
</div>;
```

Ошибка

```jsx harmony
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Button = require('../button').default;

<React.Fragment>
    <Tooltip
        placement="right"
        content={
            <div>
                <div>
                    <LoremIpsum n={3} />
                </div>
                <div>
                    <LoremIpsum n={4} />
                </div>
            </div>
        }
        theme="error"
        open
    >
        <Button>Расположение right</Button>
    </Tooltip>
</React.Fragment>;
```

Можно показывать по фокусу

```jsx harmony
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Input = require('../input').default;

<React.Fragment>
    <Tooltip enableFocusListener placement="bottom-start" content={<div>Введите номер телефона без +</div>}>
        <Input placeholder="Номер телефона" value={state.value} onChange={value => setState({value: value})} />
    </Tooltip>
</React.Fragment>;
```

Можно показывать по ховеру

```jsx harmony
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Input = require('../input').default;

<React.Fragment>
    <Tooltip
        enableHoverListener
        placement="bottom-start"
        content={<div>Введите номер телефона без +</div>}
        leaveDelay={200}
    >
        <Input placeholder="Номер телефона" value={state.value} onChange={value => setState({value: value})} />
    </Tooltip>
</React.Fragment>;
```

Можно показывать по disabled

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Button = require('../button').default;
const Checkbox = require('../checkbox').default;

<Grid container spacing={2} alignItems="center">
    <Grid item spacing={2}>
        <Tooltip enableHoverListener disabled={!state.disabled} placement="bottom" content={<div>Disabled</div>}>
            <div>
                <Button disabled={state.disabled}>Кнопка</Button>
            </div>
        </Tooltip>
    </Grid>
    <Grid item spacing={2}>
        <Checkbox
            label="disabled"
            checked={state.disabled || false}
            onChange={() => setState({disabled: !state.disabled})}
        />
    </Grid>
</Grid>;
```

Задержка при показе\скрытии

```jsx harmony
const {LoremIpsum} = require('../../styleguide/components/lorem-ipsum');
const {Grid} = require('../../styleguide/components/grid');
const Button = require('../button').default;

const getTooltip = ({enterDelay, leaveDelay}) => (
    <div style={{padding: 8}}>
        <Tooltip
            placement="right"
            content={<LoremIpsum n={3} />}
            enterDelay={enterDelay}
            leaveDelay={leaveDelay}
            enableHoverListener
        >
            <Button>{`enterDelay: ${enterDelay}, leaveDelay ${leaveDelay}`}</Button>
        </Tooltip>
    </div>
);

<div style={{width: 1000}}>
    <Grid container justify="center">
        <Grid item>{getTooltip({enterDelay: 100, leaveDelay: 100})}</Grid>
    </Grid>
    <Grid container justify="center">
        <Grid container item size={6} direction="column">
            <Grid item>{getTooltip({enterDelay: 300, leaveDelay: 300})}</Grid>
        </Grid>
        <Grid container item size={6} direction="column" alignItems="flex-end">
            <Grid item>{getTooltip({enterDelay: 300, leaveDelay: 0})}</Grid>
        </Grid>
    </Grid>
    <Grid container justify="center">
        <Grid item>{getTooltip({enterDelay: 0, leaveDelay: 300})}</Grid>
    </Grid>
</div>;
```

```js noeditor
const Radiobox = require('../../Radiobox').default
const Checkbox = require('../../Checkbox').default

const Button = require('./').default

const {default: Grid, Unit} = require('../Grid')

const size = ctx.Radiobox({state, setState, name: 'size', checked: 'm'});
const look = ctx.Radiobox({state, setState, name: 'look', checked: 'normal'});
const disabled = ctx.Checkbox({state, setState, name: `disabled`, checked: false})

const rounds = [true, true, true, true]

const round = rounds.map((val, i) => (
  ctx.Checkbox({state, setState, name: `round-${i}`, checked: val})
))

initialState = ctx.utils.initState(
  size,
  look,
  disabled,
  ...Object.values(round)
)

const sizes = ['s', 'm'].map(value => ({
  label: value,
  value: value,
  checked: size.value === value,
}))

const looks = ['normal', 'accent'].map(value => ({
  label: value,
  value: value,
  checked: look.value === value,
}));

<Grid>
  <Unit>
    <Text bold size="xs">size</Text>

    <Radiobox
        onChange={size.onChange}
        buttons={sizes}
    />
  </Unit>

  <Unit>
    <Text bold size="xs">look</Text>

    <Radiobox
        onChange={look.onChange}
        buttons={looks}
    />
  </Unit>

  <Unit>
    <Text bold size="xs">disabled</Text>

    <Checkbox
      checked={disabled.value}
      onChange={disabled.onChange}
    />
  </Unit>

  <Unit>
    <Text bold size="xs">round</Text>

    {['top-left', 'top-right', 'bottom-right', 'bottom-left'].map((val, i) => (
      <Unit>
        <span>{val}:</span>
        <Checkbox
          checked={round[i].value}
          onChange={round[i].onChange}
        />
      </Unit>
    ))}
  </Unit>

  <Unit>
    <Button
      disabled={disabled.value}
      look={look.value}
      size={size.value}
      round={round.map(x => x.value)}
    >
      Button with size {size.value.toUpperCase()}
    </Button>

  </Unit>
</Grid>
```

Try it by yourself:

```js
const Button = require('./').default;
const {default: Grid, Unit} = require('../Grid');

<div>
  <Button round={[true, false, false, true]}>Button 1</Button>
  <Button round={[false, true, true, false]}>Button 2</Button>
</div>
```

ellipsis - текст отображается в одну строку и при нехватке места заканчивается с многоточием, значение `title` по умолчанию берется `children`, но можно задать и руками, особенно это нужно делать, когда ребенком кнопки является другой элемент.
```js
const Button = require('./').default;
const {default: Grid, Unit} = require('../Grid');

const style = {
    maxWidth: '200px',
    height: '140px',
    display: 'flex',
    flexDirection: 'column',
    justifyContent: 'space-between'
};

<div style={style}>
    <Button ellipsis>Очень много текста, не помещается в одной кнопке</Button>
    <Button ellipsis>
        <span>span внутри кнопки, плохой title</span>
    </Button>
    <Button ellipsis title="заданный title">
        <span>span внутри кнопки, руками заданный title</span>
    </Button>
</div>
```

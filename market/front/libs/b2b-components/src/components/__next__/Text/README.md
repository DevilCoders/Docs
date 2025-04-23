```js noeditor
const Radiobox = require('../../Radiobox').default
const Checkbox = require('../../Checkbox').default

const {default: Grid, Unit} = require('../Grid')

const Text = require('./').default

const size = ctx.Radiobox({state, setState, name: 'size', checked: 'm'});
const bold = ctx.Checkbox({state, setState, name: 'bold', checked: false});

initialState = ctx.utils.initState(size, bold)

const sizes = ['xs', 's', 'm', 'l', 'xl'].map(value => ({
  label: value,
  value: value,
  checked: size.value === value,
}))

;

<Grid>
  <Unit gap={4}>
    <Text weight="bold" size="xs">size</Text>

    <Radiobox
        onChange={size.onChange}
        buttons={sizes}
    />
  </Unit>

  <Unit gap={4}>
    <Text weight="bold" size="xs">bold</Text>

    <Checkbox checked={bold.value} onChange={bold.onChange} />
  </Unit>

  <Unit>
    <Text weight={bold.value ? 'bold' : 'normal'} size={size.value}>
      Text with size {size.value.toUpperCase()}.
    </Text>
  </Unit>
</Grid>
```

Try it by yourself:

```js
<Text>Sandbox</Text>
```

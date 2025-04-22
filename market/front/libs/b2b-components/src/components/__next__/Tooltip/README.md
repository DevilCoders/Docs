Тултип

```jsx
const {default: Tooltip} = require('./');
const {default: Grid, Unit} = require('../Grid')
const {default: Icon, question} = require('../../Icon');

const look = ctx.Radiobox({state, setState, name: 'look', checked: 'dark'});

initialState = ctx.utils.initState(look);

const looks = ['dark', 'levitan', 'light'].map(value => ({
  label: value,
  value: value,
  checked: look.value === value,
}));

const Toggler = (props) => (<Icon {...props} style={{cursor: 'pointer'}} src={question} />);

<Grid>
  <Unit>
    <Text bold size="xs">look</Text>

    <Radiobox
      onChange={look.onChange}
      buttons={looks}
    />
  </Unit>

  <Unit>
    <Tooltip look={look.value} side="bottom" toggler target={Toggler}>
      Hey how are you?!
    </Tooltip>
  </Unit>
</Grid>
```
